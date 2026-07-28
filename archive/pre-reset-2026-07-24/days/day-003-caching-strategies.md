```
⚔ LV.1 E · XP 30/100 · streak 2🔥 ❄
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: Nothing logged. Streak held ❄ (freeze token spent — last one for the month).
```

# 📅 Day 003 — Level 1 (System Design): Caching strategies
Progress: 7/82 · Level 1 [▓░░░░]  |  Next: CDN & edge

Nothing landed in the log since Day 002 — no inbox line, no `my-progress/` file. The freeze
token covered it, but it was the only one this month. The next silent day breaks the streak
for real. No study evaluation to give — nothing new to read.

## Caching strategies

A cache is a smaller, faster store sitting in front of a slower source of truth (disk, DB,
upstream API), trading a little staleness for a lot of latency and load reduction. Three
write patterns matter: **cache-aside** (app checks cache, falls through to source on miss,
then fills the cache — most common, lazy), **write-through** (every write goes to cache and
source together — always fresh, slower writes), **write-back** (write hits cache only, source
updated later, async — fast writes, risk of loss on crash). Eviction policy decides what gets
evicted when full: LRU (recency), LFU (frequency), or TTL (time-based staleness bound).

**The one failure mode that bites in production: cache stampede.** A hot key expires, and
every concurrent request piles onto the source simultaneously to refill it — the cache meant
to protect the source becomes the reason it falls over. Fix with request coalescing (one
thread refills, others wait), soft-TTLs (serve slightly stale while refreshing in background),
or jittered expiry so keys don't all die at once.

```
client → [cache] --miss--> [source of truth]
            |                    |
          hit? <---- fill -------┘
```

**AI-infra link:** the KV-cache in LLM inference *is* a cache — storing attention
keys/values so each new token doesn't recompute over the whole context. Same tradeoffs
apply one layer up: prompt/semantic caching for LLM APIs (cache a response by prompt hash
or embedding similarity) faces the identical staleness-vs-cost tradeoff, and a stampede
on a popular cached prompt looks exactly like the classic DB-cache stampede — same fix
(request coalescing on cache miss).

## 🔁 Re-entry (15 min)

Pick ONE: read the cache-aside vs write-through section of any solid systems-design primer
(e.g. the caching chapter of "System Design Interview" or a reputable engineering-blog
writeup — verify it exists before citing it, don't take my word for a title) — OR open any
side project and find one place a cache-aside pattern would help, sketch it in one sentence.
Either counts. 15 minutes, no more.

## ✍️ Log it

One line, either place, resumes the System immediately:
- `life-rpg/log.md`: `- 2026-07-25 re-entry — 15 min on caching`
- or a file in `my-progress/` if you actually did the reading/sketch

The streak doesn't care which topic or how deep — it cares that one line lands today.
