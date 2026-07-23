⚔ LV.1 E · XP 25/100 · streak 1🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: +25 XP (Awakening — character created, System initialized). Streak held.

# 📅 Day 001 — Level 0 (Foundations): Machine model · Networking · Complexity & core data structures
Progress: 0/82 · Level 0 [░░░░░░]  |  Next: Concurrency basics — locks, atomics, async, races

## Machine model — CPU, memory hierarchy, processes vs threads

A CPU executes instructions fastest out of L1/L2/L3 cache, only falling back to RAM when it must — each level is roughly an order of magnitude slower and bigger than the one before (L1 ~1ns, L2 ~4ns, L3 ~15ns, RAM ~100ns). Programs that access memory sequentially run far faster than ones that jump around, because the CPU prefetches whole cache lines (~64 bytes) ahead of use — locality isn't an optimization detail, it's the difference between hitting cache and eating a 100x stall. A process is an isolated address space with its own memory, file descriptors, and at least one thread; threads within a process share that address space and heap but each get their own stack and registers. Key tradeoff: threads are cheap to spawn and share memory for free — but that sharing is exactly what causes races when two threads mutate the same memory without synchronization.

**AI-infra link:** KV-cache and attention buffers in LLM serving are laid out so GPU memory access stays sequential — the same locality principle, scaled to VRAM bandwidth instead of L1/L2.

```
CPU → L1(1ns) → L2(~4ns) → L3(~15ns) → RAM(~100ns)
```

## Networking — sockets, TCP/IP, HTTP, DNS

A socket is an OS-level endpoint bound to an (IP, port) pair that an app reads and writes. TCP builds a reliable, ordered byte stream on top of the failure-prone IP layer via a three-way handshake (SYN → SYN-ACK → ACK), then keeps bytes in order over lossy links using sequencing, ACKs, retransmission, and congestion control. HTTP is an application-layer protocol riding on top of that stream: request/response, verbs, headers. Before any of it, DNS resolves a name to an IP by walking root → TLD → authoritative servers, cached at every resolver hop along the way (which is why DNS cache invalidation lag is a real production hazard). Key failure mode: the handshake tax — every new TCP connection costs a full round trip before a single byte of payload moves, and HTTPS adds a TLS handshake on top of that.

**AI-infra link:** every LLM API call pays this same tax; connection pooling and HTTP/2 multiplexing are why serving frameworks reuse connections instead of opening a socket per request.

```
Client --SYN--> Server
Client <--SYN/ACK-- Server
Client --ACK--> Server   (connection open, now send data)
```

## Complexity & core data structures

Big-O measures how work scales with input size n, stripping out constants: O(1) hash lookup, O(log n) balanced-tree search, O(n) linear scan, O(n log n) sort, O(n²) nested loop. Arrays give O(1) random access but O(n) insert/delete in the middle; linked lists flip that trade. Hash maps give ~O(1) average lookup by spending memory and giving up order; balanced trees (B-trees, the structure behind almost every database index) give O(log n) while keeping data sorted. Key tradeoff: a hash map's O(1) is average-case only — collisions from a weak hash function or adversarial input degrade it toward O(n), a real scan through one overloaded bucket.

**AI-infra link:** this is exactly why vector databases don't brute-force compare embeddings (O(n) per query, dead on arrival past a few million vectors) — they use approximate structures like HNSW graphs to get sublinear search, trading perfect recall for speed.

## 🛠️ Do today (~45–60 min)

- **Coding — Two Sum (Easy):** https://leetcode.com/problems/two-sum/ — solve it twice: once O(n²) brute force (nested loop), once O(n) with a hash map. Notice which one you'd have written on instinct before today.
- **Build/measure:** write a ~15-line script (any language) that sums a large array (10M+ ints) twice — once striding by 1 (sequential), once striding by 64 (skipping roughly a cache line each time). Time both. The sequential pass should win, often by several times — that's cache locality, not compiler magic.

## 🚢 Ship This (10–15 min)

`ship-public` is untouched (0/1 this week). Today's slice: if the X account isn't live yet, create it — handle + one-line bio ("0 → $300k AI infra, built in public"). Draft (or post, if ready) one line: *"Day 1 of building AI-infra expertise in public. Today: CPU cache latency, TCP handshakes, why hash maps beat trees for O(1) lookups."* Ten minutes. Done is the target, not polish.

## ✍️ Log it

- `my-progress/day-001.md`: 3–5 lines — process vs thread in your own words, what the TCP handshake actually buys you, and your Two Sum results (brute force vs hash map) plus your real numbers from the cache-stride benchmark.
- `life-rpg/log.md`: one line per real-world action today, e.g. `- 2026-07-23 45-min study block: machine model, networking, complexity` — that's what the System pays XP on, not this lesson file.

## 🔁 Recall

No earlier days to draw on yet — two on today's material instead:

1. Why does a hash map lookup degrade from O(1) toward O(n) in the worst case?
2. Why does opening a fresh TCP connection for every API request cost more than reusing one?

**Answers:**
1. Collisions — when multiple keys land in the same bucket, average-case O(1) becomes a worst-case linear scan through that bucket; a weak or adversarial-friendly hash makes this likely.
2. Every new connection pays a full three-way TCP handshake (one round trip) plus, for HTTPS, a TLS handshake (one to two more) before any actual request bytes move. Reusing a connection (keep-alive / HTTP/2) skips that repeatedly and amortizes the cost across many requests.
