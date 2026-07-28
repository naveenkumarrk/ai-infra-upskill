⚔ LV.1 E · XP 30/100 · streak 2🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: +5 XP (Basics — shower + grooming). Streak held.

# 📅 Day 002 — Level 0→1 (Foundations → System Design): Concurrency basics · Latency & estimation · Load balancing
Progress: 6/82 · Level 1 [░░░░░░]  |  Next: Caching strategies

## Concurrency basics — locks, atomics, async, races

A race condition happens when two threads read-modify-write shared state without coordination and the outcome depends on timing. A mutex gives mutual exclusion — one thread holds it, everyone else blocks — correct but serializes. Atomics use CPU-level primitives (compare-and-swap) to update memory without ever blocking a thread, cheaper under low contention but harder to reason about. Async/await is a different axis entirely: a single-threaded event loop switches between many pending operations while each waits on I/O — cooperative, not preemptive, so one CPU-bound task still stalls everyone else on that loop. Key failure mode: races don't fail reliably. A missing lock passes tests 999 times out of 1,000 and corrupts data only under real concurrent load — the classic bug that "works on my machine."

**AI-infra link:** vLLM's continuous-batching scheduler runs an async event loop interleaving hundreds of in-flight generation requests, never blocking on any single request's next-token wait.

## Latency, throughput & back-of-the-envelope estimation

Latency is how long one request takes; throughput is how many requests complete per second — they aren't reciprocals once work runs in parallel (10 workers at 100ms latency each can sustain 100 req/s, not 10). Back-of-the-envelope estimation means reasoning from memorized orders of magnitude, not guessing:

```
L1 ~1ns · RAM ~100ns · SSD read ~100µs · same-DC round trip ~0.5ms · cross-region round trip ~150ms
```

Knowing which of these dominates your request path is most of system design. Key tradeoff: batching raises throughput (more work per unit of fixed overhead) but raises per-request latency (now you wait for the batch to fill) —"just increase the batch size" is never a free win.

**AI-infra link:** throughput-vs-latency is the most-quoted tension in LLM serving — bigger batches raise GPU utilization but worsen time-to-first-token for any individual user.

## Load balancing

A load balancer sits in front of N backend instances and spreads requests so no single one saturates. Round robin cycles blindly; least-connections routes to whichever instance has the fewest active requests right now — better when request cost is uneven. Layer 4 (TCP-level, fast, no payload inspection) vs Layer 7 (HTTP-aware, can route on path or header, costs more CPU per request). Health checks pull unhealthy instances out of rotation automatically. Key failure mode: sticky sessions — pinning a client to one backend — quietly break the "any instance can serve any request" assumption that makes balancing work; a hot server can't shed load if its sessions are glued there.

```
        ┌─> Server A (idle)      <- least-connections picks A
Client ─┼─> Server B (busy)
        └─> Server C (idle)
```

**AI-infra link:** GPU-aware routing for LLM inference balances by which node already holds the relevant KV-cache prefix, not round robin — cache locality beats naive evenness.

## 🛠️ Do today (~45–60 min)

- **Coding — Print Zero Even Odd (Medium):** https://leetcode.com/problems/print-zero-even-odd/ — three threads coordinating via locks/semaphores to print `010203...`. This is today's concurrency topic made concrete: get it wrong and you'll see the race firsthand.
- **Build/measure:** on your own machine, time three things: 1M in-memory dict lookups, a local file read (cold vs warm cache), and a network round trip (`ping`/`curl` to any public API). Compare your real numbers against the latency table above — see how close reality tracks the canonical orders of magnitude.

## 🚢 Ship This (10–15 min)

`ship-public` is still 0/1 this week. If the X account went live yesterday, post today's line now; if not, that's the blocker — clear it before anything else. Draft: *"Day 2: concurrency races, why batching trades latency for throughput, and why sticky sessions break load balancers. Solved LeetCode's Print Zero Even Odd — three threads, one shared counter, zero tolerance for races."* Bonus 5 min if time allows: push yesterday's Two Sum + cache-stride benchmark to a public gist or repo — first visible proof-of-work for the week's artifact.

## ✍️ Log it

- `my-progress/day-002.md`: 3–5 lines — your own words on what makes a race condition "non-deterministic," your Print Zero Even Odd approach (locks vs semaphores vs condition variables), and your three real latency measurements vs the canonical table.
- `life-rpg/log.md`: one line per real-world action today, e.g. `- 2026-07-24 45-min study block: concurrency, latency/throughput, load balancing` — that line is what the System pays XP on, not this file.

## 🔁 Recall

1. Why does sequential memory access beat strided access even though both touch the same number of bytes? (Day 001 — machine model)
2. Why does reusing a TCP connection save more than one round trip compared to opening a fresh one per request? (Day 001 — networking)

**Answers:**
1. The CPU prefetches whole cache lines (~64 bytes) ahead of use during sequential access, so most reads hit L1/L2; strided access with a large-enough stride skips past what got prefetched, forcing a fresh, slow trip to RAM (~100ns) on nearly every access.
2. Every new TCP connection pays a full three-way handshake (one round trip), and HTTPS adds a TLS handshake (one to two more) before any request byte moves — reusing a connection pays that cost once and amortizes it across every subsequent request instead of repeating it each time.
