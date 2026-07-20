# 🚀 Upskill Day 1 — Phase 1 System Design · Week 1 Day 1: Latency, Throughput & Back-of-the-envelope estimation

This is Day 1 — the first entry in `days/`. No prior lessons exist yet, so Section 10 below is seeded from the roadmap instead of reviewing past material. Every future day builds forward from here; nothing here will be re-taught verbatim.

---

## SECTION 1 — Coding Block (30–45 min)

**Interview Problem 1 — [LeetCode 232: Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)** (Easy)
Why it matters today: every latency/throughput system you'll design this week is built on queues — request queues in front of a thread pool, message queues between services, the KV-cache request queue in an LLM server. This problem forces you to understand *why* FIFO ordering costs you amortized work when your only primitive is LIFO, which is exactly the kind of "what does this data structure actually cost me" thinking you need before you can reason about latency.
Hint: keep two stacks — an `in` stack for pushes and an `out` stack for pops; only reverse `in` into `out` when `out` is empty.
Expected optimal complexity: O(1) amortized per operation, O(n) worst case for a single pop (n = queue size).

**Interview Problem 2 — [LeetCode 3: Longest Substring Without Repeating Characters](https://medium.com/@davoud.badamchi/solving-leetcode-problem-3-longest-substring-without-repeating-characters-from-brute-force-to-6cb42f15beca)** (Medium, sliding window)
Why it matters today: sliding-window is the exact algorithmic shape you use to compute a *rolling* throughput or error-rate metric in production ("requests in the last 60s"). Solving it teaches you to maintain window invariants incrementally instead of recomputing from scratch — the same discipline behind a real rate limiter or a rolling p99 tracker.
Hint: maintain a hash map of `char → last seen index` and a left pointer that jumps forward when a repeat is found inside the current window.
Expected optimal complexity: O(n) time, O(min(n, charset size)) space.

**Systems Coding Exercise — Streaming Latency Percentile Tracker (not LeetCode)**
Build a small class `LatencyTracker` that ingests latency samples (in ms) one at a time from a stream and can report p50/p95/p99 on demand, without storing every sample forever.
- v1 (30 min): fixed-size circular buffer of the last N=10,000 samples; on query, copy, sort, index. O(N log N) per query — good enough to understand the *definition* of a percentile before optimizing.
- v2 (stretch): replace the buffer with fixed-width histogram buckets (e.g., exponential buckets like OpenTelemetry's default set — this is literally how Prometheus histograms and HdrHistogram work). Insertion becomes O(1) (increment a bucket counter); percentile becomes an interpolated bucket-boundary lookup instead of an exact value.
Why production engineers build this: you cannot ship "average latency" to a dashboard and call it observability — averages hide the tail that hurts users (Section 3). Every serving stack you'll ever operate (nginx, Envoy, vLLM, your own gRPC service) exposes exactly this structure internally. Interviewers use this exercise to check whether you understand that percentiles are *approximated* in production, not looked up in a sorted array, and whether you can explain the accuracy/memory tradeoff of bucket width.

---

## SECTION 2 — Core Lesson: Latency vs. Throughput

**Definitions, precisely.** Latency is the time for *one* unit of work to complete, end to end — measured in time (ms, µs). Throughput is the *rate* at which a system completes work — measured in work/time (req/s, tokens/s, rows/s). They are related but not inversely proportional the way people assume. A system can have high throughput and high latency simultaneously (a batch pipeline processing millions of rows/sec, each row taking 2 minutes to traverse the pipeline) or low throughput and low latency (a lightly-loaded single-threaded server).

**Little's Law** is the formal bridge between them: `L = λ × W`, where `L` = average number of requests in the system (in flight), `λ` = average arrival rate (throughput), and `W` = average time each request spends in the system (latency). This holds for *any* stable queueing system regardless of arrival distribution — proven by John Little at MIT in 1961. Its practical power: if you know two of the three, you get the third for free. If your service handles λ=1,000 req/s and each request has W=200ms average latency, then on average L=200 requests are in flight at any moment — which tells you the minimum concurrency (worker threads, connections, GPU slots) you need to provision, before you write a line of capacity-planning code.

**Why the average lies.** Latency distributions in real systems are heavy-tailed, not Gaussian — a few requests take 100x longer than the median because of GC pauses, cache misses, lock contention, network retransmits, or noisy-neighbor CPU steal. So you never report a single "latency" number — you report p50 (median, "typical" experience), p95, and p99 (or p99.9 at high scale). A service that looks perfectly healthy at p50=20ms can be silently torturing 1% of users at p99=2,000ms — and at 30,000 req/s (roughly Cloudflare's edge scale), that "1%" is 300 requests every second failing your SLA.

**Tail latency amplification** is the failure mode that makes this urgent at scale: if a single user request fans out to 100 backend calls, and each backend independently has p99=10ms, the probability that *all 100* finish within 10ms is `(0.99)^100 ≈ 0.366` — so your end-to-end p99 is dominated not by any one backend's tail but by the *union* of 100 independent tails. This is the central result of Google's "The Tail at Scale" paper (Section 3).

```
Request lifecycle — where latency actually comes from:

  client          LB           queue         worker         downstream
    |              |              |             |               |
    |--- network -->|             |             |               |
    |              |--- routing -->|            |               |
    |              |              |--- QUEUE ---|               |
    |              |              |  wait time  |               |
    |              |              |  (Little's  |               |
    |              |              |   Law: L=λW)|--- compute --->|
    |              |              |             |    (I/O, lock, |
    |              |              |             |     GC, cache) |
    |              |              |             |<-- response ---|
    |<---------------------- total latency (W) ---------------------|

  Throughput (λ) = requests completing this pipeline per second.
  If λ approaches service capacity μ, queue wait time → ∞ (M/M/1 result).
```

**Why this matters for AI Infrastructure.** LLM serving is where latency and throughput become explicitly *two different metrics you must optimize separately*, not proxies for each other: **Time-To-First-Token (TTFT)** is a latency metric — how long the user waits before anything appears — dominated by prompt prefill compute and queueing for a free GPU slot. **Inter-Token Latency (ITL)** and **tokens/sec throughput** are governed by the decode loop and how many sequences you can batch concurrently (continuous batching, Week 7). These trade off directly: batching more concurrent requests raises aggregate tokens/sec throughput but raises each individual request's ITL, because the GPU is now time-slicing across more sequences. vLLM's own metrics (`vllm:time_to_first_token_seconds`, ITL histograms) exist precisely because you cannot run an inference service on an average — you provision GPU fleets against p99 TTFT SLAs while maximizing aggregate throughput per dollar. Little's Law applies directly here too: `L` (sequences in flight in the KV cache) `= λ` (request arrival rate) `× W` (average sequence lifetime) — this is exactly how you size KV-cache memory capacity against expected traffic.

---

## SECTION 3 — Production Case Study: Google — "The Tail at Scale"

Jeffrey Dean and Luiz André Barroso (Google Fellows) published ["The Tail at Scale"](https://www.barroso.org/publications/TheTailAtScale.pdf) in *Communications of the ACM*, Feb 2013 — arguably the single most cited systems paper on latency at scale, and required reading at every major infra org since. **The problem they documented:** at Google's scale, a single user-facing request (e.g., a search query) fans out to hundreds or thousands of leaf servers, and the response can't return until (nearly) all of them reply. As shown in Section 2's math, even a backend with a fast, well-behaved p99 of 10ms produces a system-level p99 of ~140ms once fanned out across 100 backends — the *tail* becomes the *median* of the aggregate.

**Why they built solutions instead of just accepting it:** at Google's scale, "rare" isn't rare — a 1-in-10,000 slow request happens thousands of times per second across the fleet, so you must engineer around variability, not just chase it away. Their key techniques, all still standard practice today:
- **Hedged requests** — send a duplicate request to a second replica if the first hasn't responded within the ~95th-percentile expected latency, and take whichever returns first, cancelling the loser. This trades a small amount of extra load (since most hedges are cancelled before they execute) for a large tail-latency reduction.
- **Tied requests** — send to two replicas simultaneously and let the servers themselves cancel the loser via a cheap cross-server signal, reducing wasted work versus naive hedging.
- **Micro-partitioning and load-shedding** — spread load across many small partitions so a single slow shard doesn't tail the whole system, and shed low-priority work under pressure rather than let queueing latency blow out for everyone.

**Tradeoffs:** hedging and tying cost extra capacity (duplicate work) to buy latency predictability — a direct cost-vs-tail-latency dial that Staff engineers must justify with real SLA/revenue math, not intuition. **Lesson:** tail latency isn't a monitoring afterthought — it's an architectural decision made at design time (how many backends does one request touch? can any of them be hedged? what's the cost budget for redundancy?).

---

## SECTION 4 — Staff Engineering Notes

- **Common failure mode:** teams optimize p50 because it's the number that looks good in a demo, while p99 silently degrades until it pages someone. Staff engineers set SLOs on p95/p99, never on average, and treat average-latency dashboards as a smell.
- **Cost implications:** hedged requests, redundant replicas, and over-provisioned capacity to protect tail latency all cost real money. The Staff-level judgment call is: what's the $/user-impact of a 200ms p99 vs. a 2s p99 for *this* product surface? A background batch job and a checkout button have wildly different tail-latency budgets — don't apply the same SLO template everywhere.
- **Scaling bottleneck to watch:** as you horizontally scale a fan-out system, tail amplification (Section 2's math) gets *worse*, not better, unless you actively engineer against it (hedging, timeouts, load shedding). Naive "just add more backends" scaling silently degrades your p99 even while your p50 stays flat — a classic gap between load-test dashboards and real user experience.
- **Monitoring maturity:** you need histograms (not just averages/counters) exported per-endpoint, per-region, per-dependency, with enough bucket resolution near your SLO threshold to detect drift before it breaches. Recording only a global average is equivalent to not measuring latency at all.
- **Capacity planning:** use Little's Law explicitly — don't guess at worker-pool or connection-pool sizes. Given target throughput λ and measured (or SLO'd) latency W, `L = λW` gives you the concurrency you must provision, with headroom for the variance you now know exists.
- **Recovery strategy:** define and test timeout + retry + circuit-breaker behavior *before* an incident, because in a fan-out system a single slow dependency without a timeout will tail-amplify into a full outage — this is precisely how many real cascading-failure incidents (Google, AWS, and others have public postmortems on this pattern) start.

---

## SECTION 5 — Interview Drill

**A. System Design Question:** "Design a URL shortener's redirect path to guarantee p99 redirect latency under 50ms globally, at 50,000 redirects/sec." *(This is a standard opener at companies like Amazon, Google, and Meta and previews Week 4 Day 1 — today you should only reason about the latency/throughput/estimation angle, not the full data model.)*

**B. Estimation Question:** "Your LLM inference service serves 500 requests/sec, average request lifetime (queued + prefill + decode) is 1.5 seconds. How many concurrent request slots (and roughly how many GPUs, assuming each GPU serves 20 concurrent sequences) must you provision?"
- Using Little's Law: `L = λW = 500 × 1.5 = 750` concurrent sequences in flight on average.
- GPUs needed ≈ 750 / 20 ≈ **38 GPUs** at *average* load — a Staff-level answer immediately adds that you must provision against p95/p99 concurrency, not average, because request arrivals are bursty (often modeled as Poisson, meaning short-term concurrency spikes well above the mean), so real provisioning is usually 1.3–2x the Little's-Law average, plus explicit autoscaling headroom.

**C. Tradeoff Question:** "When would you intentionally accept higher p99 latency instead of hedging requests to fix it?"
- When the extra hedge-induced load risks pushing the *whole fleet* into the high-latency regime under peak traffic (hedging under saturation makes things worse, not better — you're adding load precisely when you have none to spare).
- When the request is cheap to retry client-side and idempotent, so client-level retry-with-timeout is simpler and cheaper than server-side hedging infrastructure.
- When the traffic is low-priority/batch and the cost of extra compute for hedging isn't justified by the SLA (no user is waiting synchronously).

**What an excellent Staff-level answer includes (all three questions):**
- States explicit assumptions and numbers before computing (traffic pattern, peak/average ratio, request-size distribution) — never silently guesses.
- Distinguishes latency (single request experience, percentile-based) from throughput (aggregate rate) and never conflates the two in the same sentence.
- Names the specific mechanism (Little's Law, hedging, circuit breaker, load shedding) rather than saying "we'd add caching/scaling" vaguely.
- Quantifies the cost of any reliability technique (extra replicas, extra GPU-seconds) instead of treating it as free.
- Explicitly separates "average case" design from "tail case" design and states which one the SLO is actually written against.

---

## SECTION 6 — Hands-on Engineering Lab (45–60 min)

**Goal:** measure real latency and throughput of an HTTP server under load, and connect the numbers back to Little's Law — not read about it, produce your own histogram.

**Prerequisites:** any machine with a language runtime you're comfortable in (Go or Rust preferred per your language priority), plus a load generator: [`hey`](https://github.com/rakyll/hey) (Go, simplest) or `wrk` (C, more powerful scripting via Lua). Install whichever is available (`go install github.com/rakyll/hey@latest`, or `apt install wrk` / build from source).

**Steps:**
1. Write a minimal HTTP server (Go `net/http` is fastest to stand up) with one endpoint `/work` that simulates variable service time: sleep for a random duration drawn from, e.g., a mix of "fast" (5ms, 95% of requests) and "slow" (200ms, 5% of requests) — this artificially creates a realistic heavy tail.
2. Run it locally, then load-test with increasing concurrency: `hey -z 30s -c 10 http://localhost:8080/work`, then repeat with `-c 50`, `-c 200`.
3. For each concurrency level, record: throughput (req/s reported by `hey`), p50, p95, p99 latency (reported directly by `hey`'s output histogram).
4. Compute `L = λ × W` yourself from the reported average throughput and average latency at each concurrency level, and compare it to the `-c` value you actually set. They should roughly match — this is Little's Law empirically confirmed on your own data.
5. Plot (even ASCII/spreadsheet) throughput vs. concurrency. Find the concurrency level where throughput stops increasing and p99 starts climbing steeply — this is your server's saturation point (queueing theory: as λ→μ, wait time→∞).

**Success criteria:** you can point to the concurrency level where your server transitions from "latency-bound" (adding concurrency doesn't help, resources idle) to "throughput-bound" (adding concurrency raises queueing delay faster than it raises completed work) — and explain why, citing Little's Law and the tail behavior you engineered in step 1.

**Stretch goal:** wire in your Section 1 `LatencyTracker` (bucketed version) directly into the server instead of relying on `hey`'s client-side measurement, and expose it on a `/metrics` endpoint in Prometheus histogram format — this is the first building block toward Week 11 (OpenTelemetry/observability).

---

## SECTION 7 — Reading Pack

1. **Official Documentation:** [OpenTelemetry Metrics Data Model — Histograms](https://opentelemetry.io/docs/specs/otel/metrics/data-model/) — the industry-standard spec for exactly the histogram/percentile mechanics you built in Section 1.
2. **Engineering Blog:** [Cloudflare — "Performance measurements... and the people who love them"](https://blog.cloudflare.com/loving-performance-measurements/) — real production numbers on why p50 vs p99 diverge wildly at Cloudflare's edge scale.
3. **Video:** [Gil Tene — "Understanding Latency and Application Responsiveness"](https://www.youtube.com/watch?v=9MKY4KypBzg) — the canonical talk on why naive latency measurement (and naive averaging) systematically lies to you; Tene is the author of HdrHistogram, the real-world version of Section 1's exercise.
4. **Research Paper:** [Dean & Barroso — "The Tail at Scale," CACM 2013 (PDF, hosted by Barroso)](https://www.barroso.org/publications/TheTailAtScale.pdf) — read in full; this is Section 3's source and one of the most important systems papers of the last 15 years.
5. **Additional Deep Dive:** [vLLM — Metrics documentation](https://docs.vllm.ai/en/stable/design/metrics/) — see `time_to_first_token_seconds` and inter-token-latency histograms defined for a real production LLM server; this is where today's theory becomes AI-infra practice (previews Week 7).

---

## SECTION 8 — Build in Public

Push today's `LatencyTracker` implementation (Section 1) plus the load-test server and results from Section 6's lab as a small public GitHub repo or gist — include the throughput-vs-concurrency table/plot and one paragraph explaining the saturation point you found. This is a concrete, defensible artifact for a portfolio ("I benchmarked and explained real queueing behavior") that's far stronger than "I read about Little's Law."

---

## SECTION 9 — Mastery Checklist

```
□ I can explain this from first principles
□ I can implement it
□ I know production tradeoffs
□ I understand failure modes
□ I know the operational concerns
□ I can answer interview questions
□ I could teach another engineer
```

---

## SECTION 10 — Spaced Repetition

This is Day 1, so there is no "yesterday," "last week," or "last month" file yet — these questions instead check that today's foundation is solid enough to build Week 1's remaining days (Load Balancing, Caching, CDN, DNS/HTTP/gRPC, Availability/SLA) on top of.

**Q1.** Why can a system have high throughput and high latency at the same time — give a concrete example.
**A1.** Latency measures one request's total time; throughput measures completed work per unit time. A batch pipeline can process millions of rows/sec in aggregate (high throughput) while each individual row takes minutes to traverse the whole pipeline (high latency) — they're independent axes, not inverses.

**Q2.** State Little's Law and use it to explain why you can't just "add more servers" to fix tail latency in a fan-out system.
**A2.** `L = λW` (concurrency in system = arrival rate × average time in system) relates throughput and latency but says nothing about the *tail*. Adding more backends to a fan-out increases the number of independent p99 draws your request depends on, so `(1-p)^n` (probability all n finish fast) shrinks as n grows — more backends means a *worse* aggregate tail unless you explicitly engineer against it (hedging, timeouts), even though average latency per backend is unchanged.

**Q3.** Why is reporting only average latency considered a red flag by Staff engineers?
**A3.** Real latency distributions are heavy-tailed (GC pauses, cache misses, contention, retries), so the average is dominated by the common fast case and completely hides the p95/p99 tail that a meaningful fraction of real users actually experience — you need percentile histograms, not an average, to know if your SLA is actually being met.
