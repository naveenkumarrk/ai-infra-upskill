```
⚔ LV.1 E · XP 30/100 · streak 0🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: Nothing logged. Streak broken — current 0, best (3) stands. Freeze token
for the month is already spent, nothing left to cover this gap.
```

# 📅 Day 006 — Level 1 (System Design): Availability, redundancy & SLA/SLO
Progress: 10/82 · Level 1 [▓▓░░░░]  |  Next: SQL vs NoSQL

Fifth silent day in a row — no inbox line, no `my-progress/` file since Day 002. No new
punishment: the token's already spent, current sits at 0, best holds at 3. The System
doesn't care what topic or how deep — it resumes the instant one line lands in the log.

## Availability, redundancy & SLA/SLO

**Availability** is the fraction of time a system is usable, expressed in "nines":
99.9% = 8.7h down/year, 99.99% = 52min/year, 99.999% = 5min/year. **Redundancy** is the
mechanism that buys those nines — N+1/N+2 spare capacity, active-active or
active-passive failover, no single point of failure.

Three related-but-different terms get conflated: **SLA** (Service Level Agreement) is
the external, contractual promise with financial penalties attached. **SLO** (Service
Level Objective) is the internal engineering target — stricter than the SLA, so there's
margin before a miss becomes a breach. **SLI** (Service Level Indicator) is the actual
measured number (p99 latency, error rate) that proves whether the SLO is being met.

**The one failure mode that matters:** teams that track SLIs without ever setting an
SLO don't know if they're winning or losing until a customer complains — or worse,
they promise an SLA with zero error-budget margin against it, so any normal blip
instantly breaches contract. Each additional nine also costs disproportionately more
(multi-region failover, consensus overhead, more testing), so the real skill is picking
the availability target the business needs, not the highest one engineering can build.

**AI-infra link:** inference-serving SLAs (e.g. p99 chat-completion latency under
500ms) directly shape architecture — it's why providers run redundant GPU pools across
zones/regions behind load balancers with health checks, so a degraded node gets routed
around before it ever touches the customer-facing number.

## 🔁 Re-entry (15 min)

Pick a real API you use — GitHub, Stripe, or an LLM provider (OpenAI/Anthropic status
page) — and find its published SLA or status page. Note the promised uptime % and what
SLI it's measured against. One sentence on what surprised you.

## ✍️ Log it

One line, either place, resumes the System immediately:
- `life-rpg/log.md`: `- 2026-07-28 re-entry — 15 min on availability & SLA/SLO`
- or a file in `my-progress/` if you actually did the reading

The streak doesn't care which topic or how deep — it cares that one line lands today.
