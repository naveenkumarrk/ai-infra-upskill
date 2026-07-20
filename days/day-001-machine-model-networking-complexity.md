# 📅 Day 001 — Level 0 (Foundations): Machine model · Networking · Complexity & data structures

Progress: 3/82 · Level 0 [░░░░░░░░]  |  Next: Concurrency basics (locks/atomics/async) · Latency & estimation

**📊 Progress review:** Day 1 — no prior `my-progress/` logs exist yet, so there's nothing to evaluate. This lesson is the starting point.

---

### Machine model — CPU, memory hierarchy, processes vs threads

A CPU executes instructions via fetch-decode-execute, but the real performance story is memory: DRAM latency (~100ns) is roughly 100x an L1 cache hit (~1ns), so caches (L1/L2/L3) exist purely to hide that gap by keeping recently/likely-used data close to the core. Whether your code is fast is largely a question of whether its "working set" fits in cache or forces a trip to DRAM.

A **process** is an isolated address space plus its own resources (fds, memory map); a **thread** is an execution context that shares its process's address space with sibling threads. Threads are cheap to create and switch (no address-space swap) but share memory, so they need explicit synchronization. Processes are safer by isolation but pay context-switch and IPC overhead to share anything.

**Key tradeoff:** process isolation trades CPU/memory overhead for safety; thread sharing trades safety (races, need for locks) for near-zero-cost communication.

**AI-infra link:** inference servers run worker threads (not worker processes) against one loaded copy of a multi-GB model — forking a process per request would duplicate that memory footprint and blow the host's RAM.

```
CPU ↔ L1(~1ns,KBs) ↔ L2(~4ns,MBs) ↔ L3(~15ns,tens of MBs) ↔ DRAM(~100ns,GBs) ↔ SSD(~100µs,TBs)
```

### Networking — sockets, TCP/IP, HTTP, DNS

A **socket** is the OS handle binding your process to an (IP, port) endpoint for sending/receiving bytes. **TCP** builds an ordered, reliable, congestion-controlled byte stream on top of IP via a 3-way handshake (SYN → SYN-ACK → ACK) before any application data flows — reliability isn't free, it's paid for in handshake latency, retransmit timers, and head-of-line blocking (one lost packet stalls everything behind it). **UDP** skips all of that for latency-sensitive or loss-tolerant traffic. **HTTP** is a request/response protocol layered on TCP (or on QUIC/UDP for HTTP/3). **DNS** resolves a hostname to an IP *before* the socket connect even begins, adding a lookup round trip that caching/TTLs exist to amortize.

**Key failure mode:** a fresh TCP connection is deceptively slow to start — handshake + (usually) TLS handshake + slow-start ramp-up all happen before your first useful byte, which dominates latency for short-lived connections.

**AI-infra link:** LLM API gateways keep pooled, persistent TCP/TLS connections to inference backends specifically so each request doesn't re-pay handshake + slow-start tax — at p50 latencies of tens of milliseconds, that tax is huge.

### Complexity & core data structures

Big-O describes how work scales with input size *n* — it says nothing about absolute speed, so an O(n log n) algorithm can beat a "better" O(n) one for small n once constants and cache effects dominate. The four structures to know cold: **array** (O(1) index, O(n) insert/delete, contiguous → cache-friendly), **linked list** (O(1) insert/delete at a known node, O(n) access, pointer-chasing → cache-hostile), **hash table** (O(1) average lookup/insert, O(n) worst case under collisions or a bad hash), **balanced tree** (O(log n) everything, and you get ordered iteration for free).

**Key failure mode:** Big-O ignores memory layout. A "worse" O(n) array scan routinely beats a "better" O(log n) tree walk in practice, because sequential access stays in cache while tree pointer-chasing doesn't — until n is large enough that the asymptotic gap wins out.

**AI-infra link:** KV-cache lookups and request-routing tables in LLM serving stacks are deliberately kept as flat/array-like structures rather than pointer-heavy trees, because cache locality under GPU-adjacent memory bandwidth pressure matters more than shaving big-O in the small-n regime these systems actually run in.

---

**🛠️ Do today (~45–60 min):**
- **Coding task** — *TCP Echo Server* (Easy): write a TCP echo server + client in Go or Rust (per your language priority). Reference implementation pattern: Beej's Guide, "A Simple Stream Server/Client" — https://beej.us/guide/bgnet/
- **Hands-on build/measure** — Pointer-chasing memory-latency benchmark: allocate arrays from ~1KB up to ~1GB and measure random-access latency per element; you should see the L1→L2→L3→DRAM cliffs from the diagram above in your own numbers. Then benchmark array linear-scan vs hash-map lookup vs linked-list traversal at n=10 and n=1,000,000 and note where the "asymptotically worse" option actually wins.

**📚 Resources:**
- [Operating Systems: Three Easy Pieces](https://pages.cs.wisc.edu/~remzi/OSTEP/) — free, canonical, covers processes/threads/virtualization in depth.
- [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/) — free, canonical sockets/TCP reference.
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/) — complexity + data-structure operation reference.

**✍️ Log it:** in `my-progress/day-001.md`, note: which language you used for the echo server + a link/gist to the code; the actual latency numbers you measured at each cache level and whether the cliffs matched the diagram; which data-structure comparison surprised you; anything that confused you (e.g. the TCP handshake, cache-line size); time spent.

**🔁 Recall:** first day — no earlier topics yet. Starting Day 002 you'll get 2 recall questions pulling from today's material.
