# CURRENT

## Infra project — kv-arena (kicked off 2026-08-31, day 001 of v6)

Month: 2026-09

**Pitch:** The missing public benchmark of KV-cache storage backends. A runnable harness that benchmarks LMCache's remote backends (CPU RAM, SSD, Redis/Valkey, Mooncake, S3) under realistic multi-turn and agentic traffic, reporting TTFT recovery, p99 lookup/load latency, and cost per cached token. LMCache's own blog admits these comparisons only exist privately inside Tencent — nothing public exists. Findings get upstreamed as LMCache issues/PRs.

**Target repo:** github.com/naveenkumarrk/kv-arena (public)

**Definition of done:** Runnable benchmark repo whose README leads with measured numbers (≥4 backends × ≥2 workload shapes, with variance), one published writeup, and ≥1 merged upstream contribution to LMCache.

**Milestones:**
- **W1 (Aug 31–Sep 6):** First merged LMCache PR via onboarding umbrella issue #3372 (learn the codebase from inside). Local dev env: vLLM + LMCache running against CPU-RAM backend.
- **W2 (Sep 7–13):** Harness skeleton — workload generator (multi-turn + shared-prefix agentic shapes), metrics collection (TTFT recovery, lookup p99), first 2 backends measured (CPU RAM, SSD).
- **W3 (Sep 14–20):** Add Redis/Valkey + Mooncake backends; one rented GPU node for end-to-end runs; cost-per-cached-token math.
- **W4 (Sep 21–27):** Statistics pass (variance, repeats), README with the numbers up top, benchmark writeup published, findings filed upstream as LMCache issues.

## Venture — effective-cost intelligence for LLM API buyers (kicked off 2026-08-31, day 001 of v6)

Month: 2026-09

**Pitch:** Continuously measure what teams ACTUALLY pay per token across LLM providers — effective cache-hit rates on their traffic shape, silent effective-cost degradation, per-customer margin — and output dollar-denominated recommendations (restructure prompts for caching, switch provider tiers, cap unprofitable customers). Validated demand: 566-upvote Reddit analysis of provider cache-hit inconsistency ("wrecks cost predictability") with an explicit "you'd be the first stand-alone tool in the space" ask. Differentiated per validation data: sells decisions and dollars, not dashboards.

**Target repo:** github.com/naveenkumarrk/cost-intel (private)

**Definition of done:** Public provider cache-hit/effective-cost index live at a real domain, free estimator shipped, launched publicly (HN/Reddit/X posts), and a first-user metric: ≥1 paid audit ($149) or ≥100 unique index visitors with ≥5 estimator runs by strangers.

**Milestones:**
- **W1 (Aug 31–Sep 6):** Landing page + free cache-savings estimator live (Next.js, no backend needed for v1 estimator). Probe-harness design doc: how to measure provider effective cache behavior honestly and cheaply.
- **W2 (Sep 7–13):** Probe harness running against 3–4 providers; first measured index data; index page renders real numbers.
- **W3 (Sep 14–20):** $149 audit pipeline (upload usage export → effective-cost report); Stripe checkout; index expanded.
- **W4 (Sep 21–27):** Launch week — HN Show HN, the original Reddit communities, 10 direct outreach messages to people who complained in the validated threads; iterate on what converts.

## This week's ships (week of 2026-08-31, due 2026-09-06)

**Infra:** Claim and submit first LMCache PR via https://github.com/LMCache/LMCache/issues/3372 (their documented /claim flow, 2-day assignment SLA). Public artifact: the PR itself.
**Venture:** Landing page + free cache-savings estimator deployed and posted in one community thread. Distribution action: reply with the estimator link in one of the validated cache-cost complaint threads.

## Status

v6 fresh start 2026-08-31 (day 001). Nothing started yet on either track. Progress updates come ONLY from Naveen's check-in replies in the routine chat — never inferred. First brief should teach toward: LMCache codebase orientation (infra) and the blended effective-cost formula (venture).
