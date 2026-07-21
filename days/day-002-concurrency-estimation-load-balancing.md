# 📅 Day 002 — Level 0/1: Concurrency basics · Latency & estimation · Load balancing

Progress: 6/82 · Level 1 [▓░░░░░░░]  |  Next: Caching strategies · CDN & edge

**📊 Progress review:** No new entry in `my-progress/` since Day 001 (only the template README exists) — nothing to evaluate yet. 👉 One fix: log `my-progress/day-001.md` (or day-002) before the next run, even briefly, so future reviews have something to work from. The lesson content adapts based on what you actually did, not what was assigned — an empty log means no adaptation.

---

### Concurrency basics — locks, atomics, async, races

A **data race** happens when two threads access the same memory concurrently, at least one is a write, and there's no synchronization ordering the accesses — the outcome becomes undefined (not just "wrong", but compiler/CPU reordering can produce results that never make sense in any interleaving). A **lock** (mutex) prevents this by letting only one thread hold a critical section at a time — correct and simple, but threads block, and a thread that panics/hangs while holding it stalls everyone. An **atomic** operation (compare-and-swap, fetch-add) does a single read-modify-write as one indivisible hardware instruction — no blocking, much cheaper, but only works for single values (a counter, a pointer), not multi-step invariants across several fields. **Async** (green threads / coroutines/futures) is a different axis entirely: it's about not blocking an OS thread on I/O wait, multiplexing many logical tasks onto few threads — it doesn't remove the need for locks/atomics if those tasks touch shared state.

**Key failure mode:** reaching for a mutex around everything "to be safe" turns concurrent code sequential under contention (lock convoy), while reaching for atomics to avoid that often produces subtly broken code because multi-field updates aren't atomic just because each field's write is.

**AI-infra link:** vLLM's continuous-batching scheduler mutates the in-flight request queue from multiple worker threads per step — this is exactly where a wrong lock/atomic choice either serializes GPU-issue latency (mutex contention) or introduces a race that corrupts batch state (missing sync).

### Latency, throughput & back-of-the-envelope estimation

**Latency** is time-per-request; **throughput** is requests-per-second the system sustains. They aren't inverses of one concurrent work in flight: throughput ≈ concurrency / latency (Little's Law: `L = λW`), so you can raise throughput either by lowering per-request latency or by running more requests concurrently — but concurrency has a ceiling (memory, connection limits, GPU batch size) beyond which queueing makes latency explode. Back-of-the-envelope estimation means sizing a system from a few memorized constants (RAM ~100ns, SSD ~100µs, cross-region network ~100ms, 1 Gbps ≈ 125MB/s) and orders of magnitude, not precision — the goal is catching a design that's off by 1000x before you build it.

**Key tradeoff:** every latency-vs-throughput knob is really a queueing decision — batch more (raise concurrency) to raise throughput, and you necessarily raise tail latency for whoever's waiting in that batch.

**AI-infra link:** this is the core LLM-serving tension — bigger continuous-batch sizes raise GPU token-throughput but raise per-request time-to-first-token, which is why serving systems expose separate SLOs for TTFT (latency-sensitive) and total tokens/sec (throughput-sensitive).

```
throughput ≈ concurrency / latency   (Little's Law)
raise concurrency (batch size) → throughput ↑, tail latency ↑
```

### Load balancing

A load balancer distributes incoming requests across a pool of backend instances so no single one is overwhelmed. **Round-robin** cycles through backends in order — simple, fair only when every request costs about the same. **Least-connections** sends each new request to whichever backend currently has the fewest active connections — better when request cost varies wildly (a video-transcode request vs a health check). **IP-hash / consistent hashing** routes by a hash of the client (or request key) so the same client always lands on the same backend — needed for session affinity or cache locality, at the cost of uneven load if key distribution is skewed. Load balancers also do health checks, pulling dead backends out of rotation.

**Key failure mode:** round-robin under wildly uneven request costs concentrates all the expensive requests on whichever backend's "turn" it is next, creating hot spots despite "fair" distribution — the algorithm must match the actual cost variance of your workload.

**AI-infra link:** LLM gateways use least-connections (or queue-depth-aware routing) rather than round-robin, because a single inference request can hold a GPU worker busy for seconds while another finishes in milliseconds — round-robin would blindly send the next request to a backend still crunching a long generation.

---

**🛠️ Do today (~45–60 min):**
- **Coding task** — *Race Detector Demo* (Easy): write a Go program with an unsynchronized counter incremented by N goroutines, run `go run -race` to see it flagged, then fix it two ways — once with a `sync.Mutex`, once with `atomic.Int64` — and compare code + a quick benchmark of both. Reference: [Introducing the Go Race Detector](https://go.dev/blog/race-detector) and [Data Race Detector docs](https://go.dev/doc/articles/race_detector).
- **Hands-on build/measure** — Stand up 3 tiny local HTTP servers (different simulated response times, e.g. 10ms/50ms/500ms sleeps) behind NGINX configured first as round-robin, then as least-connections (`nginx.org` docs below); hammer it with a concurrent load tool (`hey` or `wrk`) and record request distribution + p50/p99 latency for each config. Before running it, back-of-the-envelope estimate the throughput and pick your `hey` concurrency accordingly using Little's Law.

**📚 Resources:**
- [Rust Atomics and Locks — Mara Bos (free online)](https://marabos.nl/atomics/) — canonical, deep, and free.
- [Latency Numbers Every Programmer Should Know (interactive)](https://colin-scott.github.io/personal_website/research/interactive_latency.html) — memorize the orders of magnitude.
- [NGINX HTTP Load Balancing docs](https://nginx.org/en/docs/http/load_balancing.html) — official, covers round-robin/least-conn/ip-hash directly.

**✍️ Log it:** in `my-progress/day-002.md`, note: your race-demo code (link/gist), what the race detector actually printed, the mutex-vs-atomic benchmark numbers; your NGINX load-distribution numbers for round-robin vs least-connections and whether they matched your Little's-Law estimate; anything that confused you; time spent.

**🔁 Recall:**
1. Why does an inference server use worker threads instead of worker processes for a loaded model? *(Threads share the process address space, so all workers serve requests against the same one in-memory copy of the multi-GB model; separate processes would each need their own copy, multiplying RAM use.)*
2. Why does a fresh TCP connection add so much latency compared to a reused one? *(Handshake (SYN/SYN-ACK/ACK) + TLS handshake + slow-start ramp-up all happen before the first useful byte — a pooled/persistent connection skips all of that, which is why gateways keep persistent connections to backends.)*
