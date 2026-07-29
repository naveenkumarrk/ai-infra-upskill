⚔ LV.1 E · XP 30/100 · streak 0🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: Nothing logged. Streak broken (freeze token already spent).

# 📅 Day 001 — Level 0 (Foundations): Machine model · Networking · Complexity & core data structures
Progress: 0/82 · Level 0 [░░░░░░]  |  Next: Concurrency basics — locks, atomics, async, races

The curriculum reset on 2026-07-24 to evidence-gated pace: no `my-progress/` entries exist yet, so this is Day 001 for real — nothing to review, nothing to advance past. It starts here.

## Machine model — CPU, memory hierarchy, processes vs threads

A CPU is fast only when it's fed from cache — L1 (~1ns) → L2 (~4ns) → L3 (~15ns) → RAM (~100ns), each level roughly an order of magnitude slower and bigger than the last. Programs that touch memory sequentially run multiples faster than ones that jump around, because the CPU pulls whole 64-byte cache lines ahead of use — locality isn't a micro-optimization, it's the gap between a cache hit and a 100x stall. A process is an isolated address space (own memory, own file descriptors) with at least one thread; threads inside that process share the heap but each get a private stack and register set. Key tradeoff: shared memory between threads is free and fast — and it's exactly what causes races the instant two threads mutate the same location without synchronization.

**AI-infra link:** GPU kernels for attention and KV-cache reads are laid out so memory access stays sequential across the batch/sequence dimension — same locality principle, scaled from L1/L2 to HBM bandwidth.

```
CPU → L1(~1ns) → L2(~4ns) → L3(~15ns) → RAM(~100ns)
```

## Networking — sockets, TCP/IP, HTTP, DNS

A socket is an OS-level endpoint bound to an (IP, port) pair that an app reads and writes through. TCP turns the lossy, unordered IP layer into a reliable byte stream via a three-way handshake (SYN → SYN-ACK → ACK), then keeps bytes in order with sequence numbers, ACKs, retransmission, and congestion control. HTTP rides on top as an application-layer request/response protocol. Before any packet moves, DNS resolves a name to an IP by walking root → TLD → authoritative servers, caching the answer at every resolver along the way — which is why stale DNS caches are a real production incident category. Key failure mode: the handshake tax. Every fresh TCP connection costs a full round trip before one byte of payload moves; HTTPS stacks a TLS handshake on top of that.

**AI-infra link:** every LLM API call pays this same tax on a cold connection — it's why serving stacks and API clients pool connections and use HTTP/2 multiplexing instead of opening a socket per request.

```
Client --SYN--> Server
Client <--SYN/ACK-- Server
Client --ACK--> Server   (connection open, now send data)
```

## Complexity & core data structures

Big-O measures how work scales with input size n, stripped of constants: O(1) hash lookup, O(log n) balanced-tree search, O(n) linear scan, O(n log n) sort, O(n²) nested loop. Arrays give O(1) random access but O(n) mid-array insert/delete; linked lists trade that the other way. Hash maps trade memory and order for ~O(1) average lookup; balanced trees (B-trees are the structure behind almost every database index) keep data sorted at O(log n). Key tradeoff: a hash map's O(1) is average-case only — a weak hash function or adversarial input concentrates keys into one bucket and degrades lookup toward a real O(n) scan.

**AI-infra link:** this is exactly why vector databases never brute-force-compare embeddings (O(n) per query, unusable past a few million vectors) — they use approximate graph/tree structures like HNSW to get sublinear search, trading a little recall for a lot of speed.

## 🛠️ Do today (~45–60 min)

- **Coding — Two Sum (Easy):** [leetcode.com/problems/two-sum](https://leetcode.com/problems/two-sum/) — solve it twice: once O(n²) with a nested loop, once O(n) with a hash map. Notice which one you'd have reached for on instinct before today.
- **Build/measure:** write a ~15-line script (Rust, Go, or Python — your call) that sums a 10M+ int array twice: once striding by 1 (sequential), once striding by 64 (skipping roughly a cache line each time). Time both. The sequential pass should win, often by several times — that's cache locality, not a compiler trick.

## 🚢 Ship This (10–15 min)

`ship-public` sits at 0/1 this week. Today's slice: if the X account isn't live yet, create it — handle + one-line bio (something like "0 → $300k AI infra, built in public"). Draft (post it if it's ready) one line: *"Day 1 of building AI-infra depth in public. Today: CPU cache latency, the TCP handshake tax, why hash maps beat trees for O(1) lookups."* Ten minutes, done beats polished.

## ✍️ Log it

- `my-progress/day-001.md`: 3–5 lines — process vs thread in your own words, what the TCP handshake actually buys you, and your Two Sum results (both approaches) plus the real numbers from the cache-stride benchmark.
- `life-rpg/log.md`: one line per real-world action today, e.g. `- 2026-07-29 45-min study block: machine model, networking, complexity` — that's what the System pays XP on, not this lesson file.

## 🔁 Recall

No earlier days to draw on yet — two on today's material instead:

1. Why does a hash map lookup degrade from O(1) toward O(n) in the worst case?
2. Why does opening a fresh TCP connection for every API request cost more than reusing one?

**Answers:**
1. Collisions — when multiple keys land in the same bucket, average-case O(1) becomes a worst-case linear scan through that bucket; a weak or adversarial-friendly hash function makes this more likely.
2. Every new connection pays a full three-way TCP handshake (one round trip) plus, for HTTPS, a TLS handshake (one to two more round trips) before any request bytes move. Reusing a connection (keep-alive / HTTP/2) skips that repeatedly and amortizes the cost across many requests.
