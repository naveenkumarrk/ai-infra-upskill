# 📅 Day 003 — Level 1 (System Design): Caching strategies · CDN & edge · API design & protocols

Progress: 9/82 · Level 1 [▓░░░░░░░]  |  Next: Availability & SLA/SLO · SQL vs NoSQL

**📊 Progress review:** Still nothing new in `my-progress/` — two lessons in a row with no logged work now (see `reviews/review-003.md`). ⚠️ Gap: the Day 001/002 tasks (race demo, mutex-vs-atomic bench, NGINX load-balancing measurement) have no recorded outcome. 👉 Log even a rough note in `my-progress/day-00N.md` before next run — the lesson can't adapt to what it can't see.

---

### Caching strategies

**Cache-aside** (lazy loading): the app checks the cache first; on a miss it reads the DB and populates the cache itself. **Write-through**: writes go to the cache and DB synchronously — cache is always current, but every write pays DB latency. **Write-behind** (write-back): writes hit the cache immediately and flush to the DB asynchronously — fastest writes, but a cache-node crash before flush loses data. Eviction policy (LRU, LFU, FIFO) decides what leaves when the cache is full; TTL bounds staleness independently of eviction.

**Key tradeoff:** cache-aside is resilient — if the cache dies, the DB is still the source of truth and the cache just repopulates — but every miss pays full DB latency. Write-behind removes that penalty but trades away durability.

**AI-infra link:** an LLM's KV-cache is a cache-aside structure — reusing computed attention keys/values avoids recomputation, and evicting old KV blocks under memory pressure (e.g. vLLM's PagedAttention block manager) is literally LRU eviction applied to GPU memory instead of RAM.

### CDN & edge

A CDN is a globally distributed set of edge servers (PoPs) that cache content close to users, cutting round-trip time versus hitting a single origin. Static assets cache well via `Cache-Control`/`max-age`: origin sets the TTL, edge serves hits directly and only re-fetches on miss or expiry — `stale-while-revalidate` avoids a thundering herd of origin requests the instant a popular object expires. Modern CDNs also run compute at the edge (Cloudflare Workers, Fastly Compute@Edge) — auth, A/B routing, even light inference — without a round trip to origin.

**Key failure mode:** caching personalized/dynamic content with a wrong cache key (e.g. forgetting `Vary: Authorization`) serves one user's response to another — a cache-key collision, not a security bug in the app itself.

**AI-infra link:** LLM gateways use edge PoPs to terminate TLS and do auth/rate-limiting near the user, but the generation request still has to reach a specific region with GPU capacity — the CDN speeds up everything around inference except the one thing that dominates latency: token generation itself.

### API design & protocols (REST / gRPC / WebSockets)

**REST** models resources as URLs with HTTP verbs (GET/POST/PUT/DELETE) and JSON bodies — simple, human-readable, and GET requests fit HTTP caching semantics for free. It's chatty (one request per resource) and has no native streaming (SSE/long-polling are bolted on). **gRPC** defines typed services in Protobuf, compiles to client/server stubs, and runs over HTTP/2 — true bidirectional streaming, many calls multiplexed on one connection, smaller binary payloads — at the cost of human-readability and needing a gRPC-Web bridge for browsers. **WebSockets** open one persistent full-duplex socket for continuous server push (chat, live updates), breaking the request/response assumption both REST and unary gRPC share.

**Key tradeoff:** REST's simplicity/cacheability is what you give up for gRPC's speed/typing — REST for public/browser-facing APIs, gRPC for internal service-to-service calls, WebSockets when the server must push unprompted.

**AI-infra link:** token streaming from an LLM (OpenAI-style SSE, or an internal gRPC server-streaming call) is exactly what plain REST request/response can't express — "REST" LLM APIs actually bolt on Server-Sent Events for streaming rather than staying REST-pure.

```
REST:      client → [request] → server → [full JSON response]
SSE/gRPC:  client → [request] → server → [chunk][chunk][chunk]...  (stream)
WebSocket: client ⇄ [persistent socket] ⇄ server   (either side pushes anytime)
```

---

**🛠️ Do today (~45–60 min):**
- **Coding task** — *LRU Cache* ([LeetCode 146](https://leetcode.com/problems/lru-cache/), Medium): implement `get`/`put` in O(1) using a hash map + doubly linked list. This is the exact eviction mechanism behind cache-aside caches and vLLM's KV-cache block manager.
- **Hands-on build/measure** — Put NGINX in front of a deliberately slow origin (a tiny HTTP server that sleeps 500ms per request) with `proxy_cache` enabled and a short TTL. Hit it once (cold MISS, ~500ms), hit it again (warm HIT, <5ms), check the `X-Cache-Status` header, then wait past TTL and confirm it goes back to MISS. This is caching + CDN/edge in one measurable setup.

**📚 Resources:**
- [AWS — Caching patterns (cache-aside / write-through / write-behind)](https://docs.aws.amazon.com/whitepapers/latest/database-caching-strategies-using-redis/caching-patterns.html)
- [Cloudflare Learning Center — What is a CDN?](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)
- [Google Cloud API Design Guide](https://docs.cloud.google.com/apis/design) — resource-oriented REST design used across Google's own APIs.

**✍️ Log it:** in `my-progress/day-003.md`, note: your LRU Cache solution (link), whether it passed with O(1) get/put; your NGINX cache MISS vs HIT latency numbers and what `X-Cache-Status` showed after TTL expiry; anything that confused you (eviction vs TTL, or REST vs gRPC tradeoffs); time spent.

**🔁 Recall:**
1. Why does raising continuous-batch size raise GPU token-throughput but hurt time-to-first-token? *(Little's Law — throughput ≈ concurrency/latency, so a bigger batch raises concurrency and thus throughput, but each request now waits for the whole batch to be assembled/scheduled before its first token comes back, raising per-request latency.)*
2. Why is round-robin a bad load-balancing choice for an LLM inference pool? *(Request cost varies hugely — one generation can hold a GPU worker busy for seconds while another finishes in milliseconds — round-robin ignores that and creates hot spots; least-connections or queue-depth-aware routing accounts for actual in-flight cost.)*
