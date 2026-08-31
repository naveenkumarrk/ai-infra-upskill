# ☀️ Day 001 — 2026-08-25 (Tuesday)

**Commits (24h):** infra `kv-arena`: 0 (repo not created yet) · venture `cost-intel`: 0 (repo not created yet)
**This week's ships (due 2026-08-30):** infra: not started · venture: not started

## 📌 Projects

Both tracks are active per `projects/CURRENT.md` — no market scan needed.

- **Infra (kv-arena):** W1 milestone is a first merged LMCache PR via onboarding issue [#3372](https://github.com/LMCache/LMCache/issues/3372). Nothing started; today's move is reading the storage-backend code and posting the claim.
- **Venture (cost-intel):** W1 milestone is the landing page + free estimator. The core isn't UI — it's the effective-cost math. Write the formula first.

Day 1 with zero commits isn't a red flag — but nothing exists yet on either track. Both Ship This actions below fit inside 30 minutes total.

## 📚 Lesson

### LMCache before claiming #3372: the storage-backend contract

The one abstraction every LMCache backend (CPU RAM, SSD, Redis, Mooncake, S3) implements is the storage-backend interface — essentially `put` / `get` / `contains`. `LMCacheEngine` sits above it and decides *what* to cache and *when*; the backends only decide *where bytes live and how fast they come back*. A first-PR issue is almost always a gap inside that contract — a missing edge case, an inconsistent behavior between two backends, a lifecycle bug — not a new backend. So read the interface definition plus two concrete implementations (CPU RAM and SSD are the simplest pair) before reading #3372 too literally: you want to recognize *which layer* the issue lives in before you claim it.

**Apply it today:** open the LMCache repo, find the storage-backend interface and skim the CPU-RAM and SSD implementations side by side. Then read #3372 and post the claim comment.

### Effective cost ≠ list price

Cache reads are billed at roughly 0.1× the base input price (Anthropic) to ~0.5× (OpenAI) — but cache *writes* cost a premium, roughly 1.25×–2× base depending on provider and TTL. That means caching is not automatically savings: with a low reuse rate or a short TTL, you pay the write premium without ever collecting the read discount — caching can *raise* the bill. The blended effective cost per token is therefore a function of hit rate, write rate, and the provider's specific multipliers. That formula — not any dashboard — is the actual product of cost-intel.

**Apply it today:** write the blended-effective-cost function as a plain TypeScript function with three worked test cases: a clear win (high reuse), break-even, and net-negative (low reuse, short TTL). No UI until this is right.

## 🚢 Ship This

- **Infra (10–15 min):** read [LMCache #3372](https://github.com/LMCache/LMCache/issues/3372) fully and post the claim comment.
- **Venture (10–15 min):** write the blended-effective-cost function + 3 test cases (win / break-even / net-negative). No UI yet.

## 📡 Market pulse

No signal today — nothing confirmed from the last ~72h that changes a decision.
