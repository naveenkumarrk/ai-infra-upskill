```
⚔ LV.1 E · XP 30/100 · streak 0🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: Nothing logged. Streak broken — the freeze token was already spent covering
07-24, nothing left to cover 07-25. Current reset to 0, best (3) stands.
```

# 📅 Day 004 — Level 1 (System Design): CDN & edge
Progress: 8/82 · Level 1 [▓░░░░]  |  Next: API design & protocols

Third silent day in a row — no inbox line, no `my-progress/` file since Day 002. Warned
about this on Day 003: the token only covers one gap a month. It's spent. Streak is 0
now, best stays at 3. No punishment beyond that — the System doesn't take XP away for
resting, but it doesn't pretend the gap didn't happen either. One line today ends it.

## CDN & edge

A CDN is a network of geographically distributed servers (edge PoPs) that cache and serve
content close to the user, cutting the round-trip that would otherwise cross continents to
hit an origin server. Two things get pushed to the edge: **static assets** (images, JS, CSS,
video — cached by URL, invalidated by cache-busting filenames or explicit purge) and
increasingly **compute** (edge functions — Cloudflare Workers, Fargate-at-edge style
patterns — running small request-handling logic in the PoP itself, not just files).

**The one failure mode that matters: cache invalidation is the hard part, not caching.**
Push a bad deploy and every edge node may keep serving stale or broken content for its TTL
window unless you can purge fast and everywhere — "there are only two hard problems in
computer science: cache invalidation and naming things" is a cliché because it's true here.
Anycast routing (same IP announced from many PoPs, BGP routes the client to the nearest one)
is what gets the request to the right edge node in the first place, no client-side logic
needed.

```
client --(anycast/DNS)--> nearest edge PoP --cache miss--> origin
                              |                                |
                            hit? <------------ fill -----------┘
```

**AI-infra link:** edge compute is where small, fast inference (embedding a query,
running a lightweight classifier, guardrail checks before hitting the real LLM) increasingly
lives — same latency-vs-freshness tradeoff as static-asset caching, but the "content" being
cached is a model's output. Semantic response caching for LLM APIs is CDN caching one layer
up: cache by prompt-embedding similarity instead of exact URL match, same invalidation pain
when the underlying model or system prompt changes.

## 🔁 Re-entry (15 min)

Pick ONE: read the CDN chapter of any solid systems-design primer (verify a specific title
exists before trusting it — don't take a fabricated one) — OR look up how Cloudflare or
Fastly describe their edge network architecture on their own engineering docs and note the
one thing that surprised you, one sentence. Either counts. 15 minutes, no more.

## ✍️ Log it

One line, either place, resumes the System immediately:
- `life-rpg/log.md`: `- 2026-07-26 re-entry — 15 min on CDN & edge`
- or a file in `my-progress/` if you actually did the reading

The streak doesn't care which topic or how deep — it cares that one line lands today.
