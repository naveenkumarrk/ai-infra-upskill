# From junior web SDE in Chennai to a hireable LLM inference infrastructure engineer, in 6 months

**Version 7. Written 2026-09-04. Covers 2026-09-07 to 2027-02-28, with a hard checkpoint in March 2027 and gates through 2028.**

This is the whole plan in one document. It replaces the daily coaching routine, the two-track project engine, and every earlier roadmap in this repo. There is nothing else to read. Every price, version, salary band and job requirement below was checked against the live source on 2026-09-04, and where a widely repeated number did not survive checking, the document says so instead of repeating it.

It is written for one person: 22, Chennai, about a year into a 9 LPA junior role at a startup, strong on TypeScript and web, zero shipped infrastructure work in public, roughly 13 focused hours a week, a Mac, no savings, and a stated goal of being recruited by US or other non-Indian companies into the $300k tier. It is not written for anyone else and does not pretend to be.

---

## 0. Read this first: the honest math

### What you asked for, and what six months can actually buy

You said the goal is $300k to $350k by March 2027. Here is what the evidence says about that, and then what the evidence says you can actually have.

**Where $300k base exists right now (all verified 2026-09-04):**

| Company and role | Base band | Where | Level |
|---|---|---|---|
| Anthropic, Staff/Senior SWE Inference | $320k to $485k | SF, NYC, Seattle, in office 25%+ | Senior/Staff |
| NVIDIA, Senior SWE TensorRT-LLM (L5) | $224k to $356k | Santa Clara, in-office or remote US | Senior |
| Groq, Senior Staff SWE Inference Systems | $249k to $336k | Palo Alto, remote US | Senior Staff |
| Together AI, Staff SWE Inference/Compute Infra | $240k to $280k | SF | Staff |
| Databricks, Staff SWE Model Serving | $192k to $260k | SF | Staff, 10+ years stated |

Every one of those is a senior or staff role and every one is physically in the US. The mid-level bands at the same companies are lower: Together ML Engineer Inference $160k to $230k, Fireworks Performance $175k to $220k, Red Hat vLLM $136k to $225k, Perplexity Inference $190k to $240k. All in the US.

**What India-resident engineers at non-Indian companies actually earn (levels.fyi, updated 2026-09-03):**

| Company (remote or India office) | Level | Total comp in USD |
|---|---|---|
| Coinbase (remote-first) | IC3 / IC4 / IC5 / IC6 | $48k / $83k / $129k / $215k |
| Atlassian | P50 Senior | ~$124k |
| Automattic | Senior | ~$114k |
| GitLab | Intermediate / Senior | $81k / $95k |
| Red Hat India (the vLLM employer) | L3 / L4 | $46k / $75k |
| NVIDIA India | IC3 / IC4 / IC6 | $65k / $99k / $230k |
| Google India | L5 / L6 | $124k / $236k |

The Pragmatic Engineer's 2025 trimodal survey of 2,078 India data points puts the senior median at US-headquartered companies at $63k, the 90th percentile at $133k, and the top at about $200k. Blind's consensus on $200k remote from India is that it "is rare, requires luck." No verified case exists anywhere in the research of an India-resident engineer under eight years of experience at $250k base.

**So the accurate statement is:** $300k requires being physically in the US, or in a top-band London or Dubai senior role, at senior level, at a high-paying inference company or a frontier lab. It is a 2029 to 2031 outcome if everything goes right, not a March 2027 outcome. Anyone who tells you otherwise is selling a course.

### What the next 18 months can realistically produce

This is the table you hold me to. Bands are for US and other non-Indian employers only, as you asked. India-only roles are excluded.

| Checkpoint | Realistic band | What unlocks it | Evidence |
|---|---|---|---|
| **March 2027** (1.5 years exp) | Remote contract $30k to $60k ($2.5k to $5k/month), or EOR employee $35k to $55k | One shipped, measured inference project. Two or three merged PRs in vLLM, SGLang or LMCache. Fifty targeted applications via LinkedIn remote filter and Wellfound. Contract and tax setup done. | Blind: $75k at 4 years; mid-band contracts $45k to $85k start at 3 years |
| **September 2027** (2 years) | Contract $50k to $90k, ceiling about $110k | Maintainer-visible OSS work. A US seed or Series A AI-infra startup with no India entity. Or Together AI's India-remote junior inference infra tier. | Blind: $110k fixed at 5 years, seed-stage AI startup, found via LinkedIn remote filter, Dec 2025 |
| **September 2028** (3 years) | India-remote $80k to $150k. Relocated: Netherlands or Germany $75k to $110k, UK $115k to $170k, Singapore $105k to $170k, UAE $118k to $200k tax-free, Canada $90k to $165k | UK Global Talent (Promise) needs a real public OSS record by 2027. Netherlands HSM needs any offer above about €52k. | Route table below |
| **2030** (5 to 6 years) | India-remote ceiling $130k to $215k. US senior $300k to $450k. UAE senior $200k to $300k tax-free | Senior at NVIDIA, Together or Anyscale class in the US, which requires a visa route started in 2027 or 2028 | Together AI US median $365k, Anyscale $300k, NVIDIA IC4 $376k |

### The exits out of India that need no Indian employer

You said no Indian jobs. That closes the most common route to US pay, which is an NVIDIA or Databricks India office followed by an L-1B intracompany transfer after one year. Noted and respected. These are the doors that remain, in order of how soon they can open:

| Route | Hard requirement | Earliest realistic | What it unlocks |
|---|---|---|---|
| **Netherlands Highly Skilled Migrant** | Any recognised sponsor offering at least €4,357/month (about €52k/year) for under-30s. Two to four weeks once you have the offer. | 2027 to 2028 with a job offer | Amsterdam SWE median about €102k |
| **UK Global Talent, Promise route** | Under 5 years experience, meet 2 of 4 criteria. Tech Nation's guidance is explicit: "standard employment without OSS of note will not meet the threshold." No employer needed. Endorsement 5 to 8 weeks. | 2027 to 2028 if the public record is real | London ML engineer median £111k, 75th percentile £168k |
| **Singapore Employment Pass** | S$5,600/month at age 23 plus COMPASS points. Needs an employer. | 2027 to 2028 | ML engineer median S$141k |
| **UAE (G42, Core42 and the labs clustering there)** | Employer offer. 0% income tax. | 2027 to 2028 | G42 SWE median about $118k; seniors $195k to $295k tax-free |
| **US H-1B** | A US employer willing to file for an offshore junior. FY2027 wage-weighted lottery odds: 15% at level 1, 31% at level 2. The $100k fee is currently struck down and unenforceable, appeals pending. | March 2028 registration at the earliest, October 2028 start | NVIDIA IC3 $315k, Anthropic entry SWE $367k |
| **US O-1A** | Three of eight criteria. Open source is explicitly recognised in current guidance. Needs maintainer-level record, talks, press. | 2029 to 2030 | US bands |

The point of this table is not to depress you. It is to show that the UK Global Talent route and the O-1A both reward exactly one thing: a real, public, recognised open-source and technical record. That is the same thing that gets you the remote contract in March 2027 and the same thing the $300k listings screen for. Every month of this roadmap builds that one asset.

### Why this roadmap and not the robotics one

You brought a well-written robotics roadmap and asked if you should switch. No. Three months of that plan are hardware with zero transfer to your target, robotics is the least remote-friendly field in tech, and the article's own India median for robotics engineers is below your current salary. The software half of it, ROS 2 as a distributed system and VLA inference on edge hardware, is parked with a date in section 10. Read that section when the date comes, not before.

---

## 1. What the job actually is, and what the listings screen for

I read fifteen live or recently closed listings at Anthropic, Together AI, Fireworks, Baseten, Red Hat, Databricks, Perplexity, NVIDIA, Groq and Anyscale. Requirements were tabulated, not summarised from memory.

### Skill frequency across 15 inference infrastructure listings

| Skill | Required | Preferred | Note |
|---|---|---|---|
| Python | 12 | — | Universal |
| A systems language: C++, Rust or Go | 10 | 3 | Rust named at Anthropic, Together, Perplexity, Groq. Go at Together (4 roles), Red Hat, Cerebras |
| Kubernetes, cloud, control planes | 10 | 1 | Operators, service mesh, GitOps now named explicitly |
| Large-scale distributed systems | 9 | — | The single most common primary requirement at $250k+ |
| Batching, KV cache, caching, routing | 6 | — | Anthropic (both roles), Red Hat llm-d, Baseten, Perplexity, Databricks |
| Profiling: Nsight, torch.profiler, py-spy | 5 | — | Fireworks, Baseten, NVIDIA, Groq |
| vLLM, SGLang, TensorRT-LLM internals | 3 | 5 | Required only at Red Hat and Baseten |
| Evals, benchmarks, reliability | 4 | 1 | Baseten wants GSM8K/MMLU automation |
| CUDA, Triton, ROCm kernels | 2 | 7 | Required only on pure performance teams |
| Quantization | 3 | 1 | Baseten, Perplexity |
| Bare metal, NCCL, InfiniBand, RoCE | 1 | 4 | Together (3 roles), Baseten |
| Temporal or Cadence plus Kafka or NATS | 2 | 1 | New in 2026 at Together |
| OSS contributions to inference engines | 0 | 4 | Fireworks, Baseten, Anyscale name it as a plus |
| Distributed training (FSDP, Megatron) | 0 | 1 | Essentially absent from inference postings |

Read that table twice. The bar is not "knows CUDA." The bar is **distributed systems judgment, a systems language beside Python, Kubernetes-shaped platform skill, and inference-specific depth in batching, KV cache and routing, with profiling as the proof.** Kernels are a differentiator on top, not the entry ticket. Distributed training is almost irrelevant for these roles.

### The north star listing

Together AI is currently hiring **Junior, Senior and Staff Software Engineer, Inference and Compute Infrastructure, remote in India** (Greenhouse job 5213325007). It is the only verified India-remote engineering posting at a top inference company. Its requirements, near verbatim:

- Go, Python or Rust
- Durable workflow orchestration such as Temporal or Cadence
- Control planes that "model state and reconcile it," meaning Kubernetes operators
- Event-driven systems: Kafka, NATS, SQS
- Nice to have: bare-metal lifecycle (PXE, Redfish, IPMI), GPU cluster software stacks (NCCL, CUDA, InfiniBand, RoCE)

Together also has a Senior Infra Agent Systems role remote in India (5+ years) and a Bangalore on-site AI Infrastructure Systems Engineer role. Cerebras has a Bangalore ML Systems Performance Engineer role. Those are the concrete first rungs at non-Indian companies, and month 4 of this roadmap is shaped directly around the junior Together posting.

The far target is Anthropic's inference roles, which want "significant experience with distributed systems," LLM inference optimization, batching and caching, Kubernetes, and Python or Rust, and which state "We do sponsor visas!" on every posting. That is a 2029 conversation, and everything here points at it.

### What is trending up and down in 2026 postings

Up: disaggregated prefill and decode serving with KV-cache-aware routing (NVIDIA Dynamo went 1.0 in March 2026, Red Hat's llm-d is CNCF sandbox, the Kubernetes Gateway API Inference Extension went GA). Serving across accelerators, not just NVIDIA. AI agents that operate GPU fleets, which is what both Together India roles ask for. Inference reliability and evals as job titles. Forward-deployed engineering, up 729% year on year. On-device and local inference.

Down or flat: frontend and mobile titles. New-grad hiring share, from 30% to 10% of hires between 2023 and 2025. Distributed training skills in inference postings. Ray-specific demand. Generic "MLOps" framing.

The open-source-to-money path is real but currently PhD-shaped: the vLLM team became Inferact with a $150M seed, SGLang became RadixArk at a $400M valuation, LMCache became Tensormesh with $24.5M, and the llama.cpp team joined Hugging Face in February 2026. Those are founders. But the llama.cpp move also took two core contributors who were not founders into full-time Hugging Face roles, Red Hat explicitly recruits on vLLM and llm-d contributions, and Weights and Biases' India-remote AI engineer role listed open-source contributions as a hard requirement. The mechanism works below founder level. It just takes eighteen months of visible work rather than six.

---

## 2. How this system works now

The daily routine is gone. You said you did not follow it, so it was dead weight. This document is the system. These are its rules.

**Time.** About 13 hours a week: 90 minutes on weekdays after work, three hours each on Saturday and Sunday. Monday to Thursday is building. Friday is reading. Saturday is the long build session. Sunday is shipping and the weekly check.

**One track.** The earlier plan ran an infrastructure project and a revenue product side by side, and in five days neither started. Thirteen hours a week does not fund two tracks. The revenue idea, an effective-cost index for LLM API buyers, survives as the month 5 public artifact because it is also legitimate inference cost engineering. It is not a separate business this year.

**Public by default.** Every project lives in a public GitHub repo from its first commit. The README leads with the measured numbers, then the architecture, then a section titled "What broke and how I fixed it." That last section is the highest-value thing a self-taught portfolio can contain because it cannot be faked from a tutorial. The venture repo from the old plan is deleted or made public; nothing private counts.

**Sunday check.** Every Sunday you append four lines to `WEEKLY.md` in this repo: what shipped and where (a link), what you measured (a number), what broke, and next week's single ship. If you cannot write a link and a number, the week did not ship. No coach reads it. You do. The file is the accountability.

**The one-question rule.** Any article, roadmap, course or new field gets one question before you spend an hour on it: does it help this month's ship? If no, it goes into `PARKED.md` with today's date and the date you will look at it again. The robotics roadmap is the first entry.

**Compute budget.** ₹4,000 a month. That is about 125 hours of an RTX 4090 on RunPod's community tier at ₹32 an hour, or 20 hours of an H100 at ₹188 an hour, or a mix. Section 9 has the full price table. You do not buy a GPU this year.

**Languages.** Python is the working language throughout. C++ starts in month 1 and stays a weekly habit because vLLM, SGLang, TensorRT-LLM and CUTLASS are Python over C++ and CUDA. Go starts in month 4 because the India-remote listings ask for it and Kubernetes operators are written in it. Rust is parked: the inference stacks you will contribute to are not Rust, and your earlier language priority list was written before the listings were read.

**Two kinds of project.** Each month has one **portfolio project**, which is public, measured, polished, and exists to get you hired. Each month also has two to four **learning projects**, which are small from-scratch builds that exist to make the theory stick: your own paged KV cache, your own continuous-batching scheduler, your own speculative decoder, your own KV-aware router. They live in one repo, `learning-lab`, one folder each, with a short README that states the number you measured. They do not need polish. They need to work and to have taught you something you can explain. Each is sized for a Friday evening or a Saturday morning, three to six hours. The portfolio ship comes first every week; a learning project is what you do after it is on track, never instead of it. Interviewers love these because "I wrote a paged KV block manager to understand vLLM's" survives three follow-ups where "I read the vLLM docs" does not.

**The fundamentals strand.** The projects above are all infrastructure-shaped on purpose, because the target job is. But a strong engineer at two years has habits a web-only junior often does not, and coding screens still filter on them before anyone opens your portfolio. So about two hours a week, every week for six months, go to four habits that are not projects:

- **One timed algorithm problem in Python and one in C++ or Go, every week.** Work through the NeetCode 150 list ([neetcode.io/practice](https://neetcode.io/practice), free), in its order: arrays and hashing, two pointers, sliding window, stack, binary search, linked list, trees, heaps, graphs, dynamic programming. Forty-five minutes each, from a blank file, no hints until the timer ends. Fifty problems by March covers every pattern an inference team's screen will ask. Concurrency-flavoured problems, which are what these teams actually prefer, come from the month 6 katas.
- **Tests on every learning project from month 2 onward.** pytest for Python, the standard `testing` package for Go, Catch2 for C++. Not for coverage. For the habit of writing the test that would have caught the bug you just fixed. The "what broke" section of each README gets stronger when a test proves the fix.
- **Read one merged pull request closely every week** in the repo you are contributing to. Not yours. Read the diff, the review comments, and what the maintainer asked to change. This is how you learn a codebase's taste faster than any docs, and it is how your own PRs start getting merged on the first review.
- **A one-page design doc before each portfolio project.** Problem, constraints, two options considered, the one chosen and why, what you will measure, what could go wrong. Half a page is fine. The discipline of writing it is what senior engineers are paid for, and every serious company will ask you to write one in the interview loop.

**No tutorial-only weeks.** Every week ends in a commit to a project repo. Reading is Friday. If a week has no commit, the following Monday's first task is the smallest commit that ends the streak.

---

## 3. Month 1: Systems foundations and your first inference engine in your hands

**2026-09-07 to 2026-10-04. Goal: run a production inference engine on rented hardware, measure it, understand the arithmetic that explains the measurements, and land one upstream pull request.**

Almost every roadmap in this space starts with "learn transformers." This one starts with running vLLM and reading its metrics, because the fastest way to make the theory stick is to have numbers you cannot explain yet. By the end of the month you will be able to say why time-to-first-token and inter-token latency behave differently under load, and you will have that explanation in a public README.

### What to learn

**1. Inference arithmetic and the KV cache**

This is the napkin math the whole field runs on: why decode is memory-bandwidth bound, why the KV cache is the thing that fills GPU memory, and why batching helps throughput until it hurts latency.

Resources:

- **kipply, Transformer Inference Arithmetic** (free). [kipp.ly/transformer-inference-arithmetic](https://kipp.ly/transformer-inference-arithmetic/). The canonical primer. Written in 2022 with A100 numbers, and the reasoning is unchanged. Read it twice and redo the arithmetic for an H100.
- **Modal GPU Glossary** (free). [modal.com/gpu-glossary](https://modal.com/gpu-glossary). The best terminology reference, covers Blackwell. Keep it open all month.
- **PagedAttention paper, vLLM** (free). [arXiv 2309.06180](https://arxiv.org/abs/2309.06180). Read sections 1 to 4 only this month. This is what you are about to run.
- **How to Scale Your Model, GPU chapter** (free). [jax-ml.github.io/scaling-book/gpus](https://jax-ml.github.io/scaling-book/gpus/). The rooflines chapter for H100, B200 and GB200, continuously revised. Read the roofline section only for now.
- **Andrej Karpathy, Let's build GPT** (free). [YouTube](https://www.youtube.com/watch?v=kCc8FmEb1nY). If you have never written attention by hand, do this in week 1. Two hours.

Focus on:

- Parameters times two bytes equals weight memory. KV cache per token equals 2 times layers times heads times head dimension times bytes. Know these cold.
- Why prefill is compute-bound and decode is memory-bandwidth-bound, and what that does to GPU utilisation at batch size 1.
- What continuous batching is and why it beats static batching.
- The three metrics that matter: time to first token, inter-token latency, and goodput under an SLO.

Practice task: compute by hand the KV cache size per token for Llama 3.1 8B in FP16, then the maximum number of concurrent 4k-token sequences that fit in a 24GB RTX 4090 alongside the weights. Write the answer down. You will check it against vLLM's own log line in week 2.

**2. Running vLLM and reading its metrics**

Resources:

- **vLLM documentation** (free). [docs.vllm.ai](https://docs.vllm.ai/en/latest/). Current release v0.28.0, August 2026. Start at Quickstart, then read the Metrics design page, which explains every Prometheus histogram vLLM exports.
- **vLLM metrics design** (free). [docs.vllm.ai/en/latest/design/metrics.html](https://docs.vllm.ai/en/latest/design/metrics.html). TTFT and ITL histograms, KV usage gauges, and a reference Grafana dashboard.
- **vLLM contributing guide** (free). [docs.vllm.ai/en/latest/contributing](https://docs.vllm.ai/en/latest/contributing/). Pre-commit hooks and DCO sign-off, which you need for the pull request in week 4.
- **llama.cpp** (free). [github.com/ggml-org/llama.cpp](https://github.com/ggml-org/llama.cpp). Runs on your Mac with Metal. This is what you use when you do not want to pay for a GPU: a local engine to poke at, not a substitute for vLLM.

Focus on:

- Serving a model with the OpenAI-compatible server, sending concurrent requests, and watching `vllm:num_requests_running`, `vllm:gpu_cache_usage_perc` and the TTFT histogram move.
- Using the built-in `vllm bench serve` to produce a throughput and latency table at three concurrency levels.
- What `--max-num-seqs`, `--max-model-len` and `--gpu-memory-utilization` actually change.
- Prefix caching: turning it on and seeing TTFT drop on shared-prefix requests.

Practice task: on a rented RTX 4090 (RunPod community tier, about ₹32 an hour), serve Llama 3.1 8B or Qwen2.5 7B, run the benchmark at concurrency 1, 8 and 32, and record TTFT p50 and p99, ITL p50 and p99, and tokens per second. Then turn on prefix caching and rerun with a shared 1,000-token system prompt. Put both tables in a README. The cost of this task is about ₹150.

**3. Python as a systems language**

You know Python. You do not yet know it the way an inference engineer needs to, which means asyncio, the profiler, and what the GIL does to a request handler under load.

Resources:

- **Python asyncio docs** (free). [docs.python.org/3/library/asyncio.html](https://docs.python.org/3/library/asyncio.html). Python 3.14. The official reference. Read the high-level API page and the event loop page.
- **Fluent Python, 2nd edition, Luciano Ramalho** (paid, O'Reilly). [fluentpython.com](https://www.fluentpython.com/). The deep-Python standard. Chapters on concurrency and asyncio are the ones that matter here. Buy if you can, otherwise the asyncio docs plus py-spy carry you.
- **py-spy** (free). [github.com/benfred/py-spy](https://github.com/benfred/py-spy). Sampling profiler that attaches to a running process. Baseten names it in their listing. Learn `py-spy top` and `py-spy record` on the vLLM server process.

Focus on:

- Writing an async load generator with `asyncio` and `httpx` that opens N concurrent streams and records per-token timestamps. You will use this all year.
- Reading a flame graph from py-spy and finding where the server spends time between GPU calls.
- Virtual environments with `uv`, which is what the vLLM repo uses.

Practice task: write your own load generator that reproduces vLLM's benchmark numbers within 10%. When it disagrees, find out why. It is usually your timestamping.

**4. C++, week one of many**

You will not write CUDA this month. You will start C++ because the engines you are learning are C++ underneath and month 3 needs you reading it comfortably.

Resources:

- **learncpp.com** (free). [learncpp.com](https://www.learncpp.com/). The most complete, actively revised modern C++ tutorial. Chapters 1 to 13 across months 1 and 2: basics, functions, references, pointers, classes.
- **cppreference** (free). [en.cppreference.com](https://en.cppreference.com/w/). The reference, not a course.

Practice task: 30 minutes on learncpp every Friday. By month end, write a C++ program that computes the same KV-cache arithmetic as your Python did, compiled with `-O2`, and reads the model config from a JSON file using nlohmann/json.

**5. Linux and the tools**

Resources:

- **MIT Missing Semester, IAP 2026** (free). [missing.csail.mit.edu](https://missing.csail.mit.edu/). The 2026 run added packaging and agentic coding. Do the shell, editors, data wrangling and command-line environment lectures.
- **Linux perf wiki** (free). [perfwiki.github.io](https://perfwiki.github.io/main/). Note the URL moved off kernel.org. You need `perf top` and `perf record` only.
- **Pro Git, 2nd edition** (free). [git-scm.com/book](https://git-scm.com/book/en/v2). Chapters 2, 3 and 5. You will be rebasing onto upstream main every week from now on.

### Month 1 learning projects

- **nanoGPT with a KV cache.** Take the model from Karpathy's "Let's build GPT" or nanoGPT and write the generation loop yourself twice: once recomputing attention over the whole sequence every step, once with a KV cache. Run both on your Mac for 512 generated tokens and plot tokens per second against sequence length. The first curve falls, the second stays flat. You now know why the KV cache exists and what it costs in memory, from your own code.
- **llm-loadgen.** The async load generator from section 3 of this month, made into a proper tool: N concurrent streams, per-token timestamps, TTFT and ITL percentiles, goodput under an SLO you pass on the command line, CSV out. You will use it every month, and reproducing vLLM's own benchmark numbers within 10% is the acceptance test.
- **memplan, in C++.** A command-line tool that reads a Hugging Face `config.json`, computes weight memory and KV bytes per token for a given dtype, and prints the maximum concurrent sequences at a given context length for a given GPU memory size. Your first real C++ program with a JSON library, a struct, and a reason to exist.
- **Optional: a BPE tokenizer.** Two hundred lines of Python that train byte-pair merges on a text file and encode and decode. Karpathy's tokenizer lecture is the guide. Useful because token counts drive every cost and memory number you will ever compute.

### The month 1 project: kv-arena, part one

kv-arena is the public benchmark of KV-cache storage backends for LMCache that does not yet exist. LMCache's own blog admits the comparisons only exist privately. The month 1 slice is the harness and the first two backends.

- **Week 1 (Sep 7 to 13):** repo exists, README states the question. vLLM plus LMCache running on a rented 4090 with the CPU-RAM backend. Baseline numbers without LMCache recorded. Claim an issue on LMCache's onboarding umbrella, issue 3372, which has a documented `/claim` flow.
- **Week 2 (Sep 14 to 20):** your async load generator produces two workload shapes: multi-turn chat with growing context, and agentic with a shared 2k-token prefix across many requests. TTFT with and without LMCache CPU-RAM, at three concurrency levels.
- **Week 3 (Sep 21 to 27):** add the local-disk backend. Measure TTFT recovery after a simulated eviction. Record variance across three runs. Your first LMCache or vLLM pull request submitted, even if it is a docs or test fix. vLLM has 10 open good-first-issues as of today; LMCache's onboarding issue lists more.
- **Week 4 (Sep 28 to Oct 4):** README rewritten to lead with a table of numbers, a diagram of the harness, and the first "what broke" section. Post the repo once on X and once in the LMCache Slack.

Total compute this month: about 25 GPU hours, about ₹800.

### Month 1 milestone

By 2026-10-04 you should be able to:

- Compute KV-cache memory for any model from its config and predict max concurrency for a given GPU.
- Serve a 7B or 8B model with vLLM on a rented GPU and produce a TTFT, ITL and throughput table at three concurrency levels.
- Explain from your own numbers why TTFT rises with concurrency faster than ITL does.
- Show a public repo with a measured baseline, two LMCache backends compared, and a submitted upstream PR.
- Attach py-spy to a running server and read the flame graph.
- Read a C++ class definition without flinching.
- Show a KV-cache-versus-no-cache tokens-per-second curve from your own nanoGPT code.

---

## 4. Month 2: Inside the serving engine

**2026-10-05 to 2026-11-01. Goal: understand vLLM's scheduler, memory manager and KV connector layer well enough to change them, finish kv-arena with four backends, and publish the writeup.**

This is the month that turns "I can run vLLM" into "I can explain what vLLM is doing and where it is wrong." It is also the month your name starts appearing in an upstream repository more than once.

### What to learn

**1. vLLM internals**

Resources:

- **vLLM design docs** (free). [docs.vllm.ai/en/latest/design](https://docs.vllm.ai/en/latest/design/). Read in this order: architecture overview, the V1 engine and scheduler, paged attention, prefix caching, then KV connectors. Then read the actual scheduler source with the doc open beside it.
- **vLLM office hours and forum** (free). [discuss.vllm.ai](https://discuss.vllm.ai) and [slack.vllm.ai](https://slack.vllm.ai). Biweekly office hours are recorded on YouTube. Watch two that cover the scheduler or KV connectors.
- **Aleksa Gordić, Inside vLLM** (free). [aleksagordic.com/blog/vllm](https://www.aleksagordic.com/blog/vllm). The best outside walkthrough of the request lifecycle.
- **SGLang docs and RadixAttention** (free). [docs.sglang.ai](https://docs.sglang.ai). Current v0.5.18. Read the RadixAttention explanation so you understand the other way to do prefix caching.
- **Chunked prefill and speculative decoding, conceptual only this month.** The vLLM docs pages on each. You will implement neither yet.

Focus on:

- The request lifecycle: tokenize, schedule, allocate blocks, prefill, decode, free.
- What the scheduler decides each step and what it is trading off.
- The block table and why a page size of 16 tokens is the default.
- How prefix caching hashes blocks and when a hit is missed.
- The KV connector interface: what LMCache plugs into, what a connector must implement.

Practice task: add a debug log line to vLLM's scheduler that prints the number of preempted sequences per step, run your month 1 benchmark at concurrency 64, and explain the preemption pattern you see in a short markdown note in the kv-arena repo. Then delete the log line.

**2. Benchmark methodology**

A benchmark nobody trusts is worse than none. This month you learn how to make one that survives review.

Resources:

- **InferenceX, SemiAnalysis** (free, Apache 2.0). [github.com/SemiAnalysisAI/InferenceX](https://github.com/SemiAnalysisAI/InferenceX). Nightly vLLM, SGLang and TensorRT-LLM runs across H100 to GB300. Read how they define workloads and report variance. They accept pull requests, and this is the best open venue in existence for someone who wants to contribute benchmark infrastructure.
- **vLLM perf-eval repo** (free). [github.com/vllm-project/perf-eval](https://github.com/vllm-project/perf-eval). How vLLM's own CI measures itself.
- **MLPerf Inference rules** (free). [mlcommons.org/benchmarks/inference-datacenter](https://mlcommons.org/benchmarks/inference-datacenter/). Read the scenario definitions for server and offline. You will not submit to MLPerf, but you will borrow its rigour.

Focus on:

- Warmup, repeat counts, and reporting p50 and p99 with the spread across runs.
- Fixing the random seed for prompts and lengths.
- Isolating one variable per table.
- Goodput: throughput that meets an SLO, which is the number companies actually buy.

Practice task: rerun your month 1 tables with three repeats and report mean and standard deviation. If any p99 varies more than 15% between runs, find out why before adding features.

**3. C++ continues**

learncpp chapters 14 to 21 across the month: classes, operator overloading, move semantics, templates. On the last Friday, read `csrc/cache_kernels.cu` in vLLM top to bottom and write down every construct you do not recognise. That list is your month 3 reading.

**4. Reading a systems design text properly**

- **Designing Data-Intensive Applications, 2nd edition, Kleppmann and Riccomini** (paid, list $69.99). [oreilly.com](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/). Published March 2026. Buy the second edition, not the first. Chapters on replication, partitioning and consistency this month, one chapter per Friday. Nine of fifteen listings said "large-scale distributed systems" before they said anything about ML.

### Month 2 learning projects

This is the month for the single most valuable learning project of the year, so the others are lighter.

- **mini-vllm.** On top of your month 1 nanoGPT, build a serving engine in about 500 lines of PyTorch: a request queue, a paged KV block manager with a block table per sequence and a free list, and a scheduler that admits new requests each step while others are mid-decode, preempting when blocks run out. Compare static batching, where a batch waits for its slowest request, against your continuous batching on a workload with mixed output lengths. Report throughput and p99 latency for both. This is PagedAttention and continuous batching from the inside, and it is the project you will talk about in every interview for two years.
- **radix prefix cache.** Add a radix tree over token prefixes to mini-vllm so requests sharing a prefix share KV blocks, the way SGLang's RadixAttention does. Measure block reuse and TTFT on your shared-prefix workload. Then break it by evicting the wrong node and watch what happens.
- **eviction simulator.** A Python simulator that replays a request trace from llm-loadgen against a fixed-size KV store under LRU, LFU and a prefix-aware policy, and reports hit rate and bytes moved. This directly informs what kv-arena should measure and gives you a reason to open LMCache's eviction code.
- **consistent hashing ring.** Two hundred lines in C++ or Python: a ring with virtual nodes, add and remove a node, count how many keys moved. The DDIA partitioning chapter made real, and the seed of the router you will build in month 4.

### The month 2 project: kv-arena, complete

- **Week 1 (Oct 5 to 11):** Redis or Valkey backend added and measured. Second upstream PR submitted, ideally a real fix surfaced by your own harness.
- **Week 2 (Oct 12 to 18):** Mooncake backend added. Mooncake is the KV-centric disaggregation store vLLM featured in May 2026, current v0.3.13. Getting it running is a real systems task and the writeup of that alone is portfolio material.
- **Week 3 (Oct 19 to 25):** one rented H100 session, about 6 hours at ₹188, for end-to-end numbers on a larger model. Cost per cached token computed for each backend from real hourly prices.
- **Week 4 (Oct 26 to Nov 1):** the writeup. Two thousand words, published on your own site or GitHub Pages, leading with the four-backend table. Findings that look like bugs get filed as LMCache issues with reproduction commands. Post on X, LMCache Slack, and r/LocalLLaMA.

Compute: about 35 GPU hours, about ₹2,500.

### Month 2 milestone

By 2026-11-01 you should be able to:

- Walk someone through a request's life inside vLLM from HTTP to freed blocks.
- Explain preemption, prefix cache misses and scheduler tradeoffs from your own measurements.
- Produce a benchmark table with repeats and spread that a maintainer would accept.
- Show four LMCache backends measured on two workload shapes, with cost per cached token.
- Point to two submitted and at least one merged upstream pull request.
- Read a CUDA source file and name what you do not understand.
- Demonstrate your own continuous-batching scheduler beating static batching on p99 latency, in code you wrote.

---

## 5. Month 3: GPU programming and quantization

**2026-11-02 to 2026-11-29. Goal: write a kernel, profile it, make it faster, and quantize a model while measuring exactly what accuracy you paid for the speed.**

Kernels are the skill everyone in this field respects and almost no self-taught candidate has. They are also, per the listings, a differentiator rather than the entry ticket. So this month is bounded: one fused kernel written in Triton, one CUDA kernel read and modified, one profiler session that changes something, one leaderboard submission, and one quantization study. That is a complete, honest month, not a career.

### What to learn

**1. GPU architecture and the programming model**

Resources:

- **Programming Massively Parallel Processors, 5th edition, Hwu, Kirk and El Hajj** (paid). [shop.elsevier.com](https://shop.elsevier.com/books/programming-massively-parallel-processors/hwu/978-0-443-43900-1). The 5th edition published June 2026 and supersedes the 4th. Chapters 1 to 6 this month: memory hierarchy, tiling, and performance considerations. GPU MODE's lectures follow this book chapter by chapter.
- **GPU MODE lectures, YouTube and Discord** (free). [github.com/gpu-mode/lectures](https://github.com/gpu-mode/lectures), [youtube.com/@GPUMODE](https://www.youtube.com/@GPUMODE), [discord.gg/gpumode](https://discord.gg/gpumode). Over 100 lectures. Watch lectures 1 to 8 (the PMPP walkthroughs), then the Triton lecture and the profiling lecture. Join the Discord and read the kernel channels daily.
- **CUDA C++ Programming Guide** (free). [docs.nvidia.com/cuda/cuda-c-programming-guide](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html). CUDA 13.3. Reference, not a course. Chapters on the programming model and memory hierarchy.
- **Aleksa Gordić, Inside NVIDIA GPUs: Anatomy of matmul kernels** (free). [aleksagordic.com/blog/matmul](https://www.aleksagordic.com/blog/matmul). September 2025. From fundamentals to PTX, TMA and wgmma. Read once now for the map, again at month end.

**2. Writing kernels**

Resources:

- **Triton tutorials** (free). [triton-lang.org](https://triton-lang.org/main/getting-started/tutorials/index.html). Triton 3.8. Do tutorials 1 to 6: vector add, fused softmax, matmul, low-memory dropout, layer norm, fused attention. This is your primary kernel language this month because it runs on your rented 4090 and is what vLLM and SGLang use for most custom ops.
- **siboehm, How to Optimize a CUDA Matmul Kernel** (free). [siboehm.com/articles/22/CUDA-MMM](https://siboehm.com/articles/22/CUDA-MMM). Ten kernels from naive to 94% of cuBLAS on FP32. The single best hands-on CUDA read. Type every kernel yourself.
- **Pranjal, Outperforming cuBLAS on H100: a worklog** (free). [cudaforfun.substack.com](https://cudaforfun.substack.com/p/outperforming-cublas-on-h100-a-worklog). The Hopper continuation with TMA and wgmma. Read, do not reproduce, unless you rent an H100 for it.
- **GPU Puzzles, Sasha Rush** (free). [github.com/srush/GPU-Puzzles](https://github.com/srush/GPU-Puzzles). Twelve puzzles in Numba. Frozen since 2024 and still the fastest way to build thread-index intuition in an afternoon.
- **CUTLASS 4.8 and the CuTe DSL** (free). [github.com/NVIDIA/cutlass](https://github.com/NVIDIA/cutlass). Python-first kernel authoring, public beta graduating. Read the CuTe DSL quickstart in the last week so you know it exists. Do not learn it this month.

**3. Profiling**

Resources:

- **Nsight Systems and Nsight Compute docs** (free). [docs.nvidia.com/nsight-systems](https://docs.nvidia.com/nsight-systems/UserGuide/index.html), [docs.nvidia.com/nsight-compute](https://docs.nvidia.com/nsight-compute/NsightCompute/index.html). Nsight Systems 2026.4, Nsight Compute 2026.2. Learn `nsys profile` for the timeline and `ncu` for per-kernel metrics. Five listings name these tools.
- **torch.profiler** (free). PyTorch 2.14 docs. How to trace a vLLM step and open it in Perfetto.

Focus on:

- Occupancy, memory coalescing, shared memory bank conflicts, and register pressure. Know what each looks like in Nsight Compute.
- Reading achieved memory bandwidth against the roofline and knowing whether your kernel is compute or memory bound.
- Fusing two kernels and measuring whether it helped, because it does not always.

**4. Quantization**

Resources:

- **llm-compressor, vLLM project** (free). [github.com/vllm-project/llm-compressor](https://github.com/vllm-project/llm-compressor). v0.13. The one quantization tool to learn: GPTQ, AWQ, SmoothQuant and FP8 or NVFP4 outputs that vLLM loads directly.
- **Papers** (free, arXiv): GPTQ 2210.17323, AWQ 2306.00978, SmoothQuant 2211.10438, FP8 formats 2209.05433. Read the method section of each, not the whole paper.
- **NVIDIA Transformer Engine FP8 primer** (free). [docs.nvidia.com/deeplearning/transformer-engine](https://docs.nvidia.com/deeplearning/transformer-engine/user-guide/examples/fp8_primer.html). E4M3 versus E5M2 and block scaling explained properly.
- **lm-evaluation-harness** (free). [github.com/EleutherAI/lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness). GSM8K and MMLU runs against a vLLM endpoint, which is exactly the automation Baseten asks for.

### Month 3 learning projects

- **CUDA from zero, four kernels.** Vector add, parallel reduction, prefix scan and a tiled matmul, each written from PMPP's description, each with achieved bandwidth or FLOPs printed and compared against the RTX 4090's roofline. The reduction and scan are not in siboehm's article and they teach shared memory and synchronisation better than matmul does.
- **roofline plotter.** A small Python script: give it a kernel's FLOPs and bytes moved and it plots the point against the roofline for the GPU you name. Every kernel you write this month gets a dot on this chart. It makes "memory bound" a thing you can see.
- **flash attention forward in Triton.** Triton tutorial 6 gives you the skeleton. Write it, then measure against PyTorch's scaled dot product attention at four sequence lengths and explain the crossover. Do not attempt the backward pass.
- **quantize by hand.** Implement per-channel INT8 weight quantization and dequantization for one Linear layer in plain PyTorch, measure output error against FP16, then run GPTQ from llm-compressor on the same layer and measure again. The gap between the two numbers is what GPTQ's Hessian trick buys, and you will remember it because you saw it.

### The month 3 project: kernel-notebook and a quantization study

One repo, two halves.

- **Week 1 (Nov 2 to 8):** Triton tutorials 1 to 4 completed and pushed with your own notes. GPU Puzzles done. Nsight Systems trace of one vLLM step captured and annotated.
- **Week 2 (Nov 9 to 15):** write a fused RMSNorm plus residual-add kernel in Triton, benchmark it against the unfused PyTorch version at four hidden sizes, profile both in Nsight Compute, and explain the difference in achieved bandwidth. Submit a kernel to a GPU MODE leaderboard at [gpumode.com](https://www.gpumode.com/) via popcorn-cli. The rank does not matter. The submission does.
- **Week 3 (Nov 16 to 22):** quantize Llama 3.1 8B or Qwen2.5 7B to FP8 and to a 4-bit format with llm-compressor. Serve each with vLLM. Table: GSM8K and MMLU accuracy, throughput at concurrency 16, TTFT p99, and GPU memory. Four rows: BF16, FP8, AWQ-4bit, GPTQ-4bit.
- **Week 4 (Nov 23 to 29):** type all ten of siboehm's kernels in CUDA, run them on the 4090, and reproduce the curve. Writeup of both halves, leading with the accuracy-versus-throughput table and the kernel bandwidth chart. Third upstream PR: a docs improvement to Triton, llm-compressor or vLLM that you noticed while doing this.

Compute: about 40 GPU hours, about ₹1,500 on the 4090, plus a 2-hour H100 session if you want the Hopper matmul numbers, about ₹400.

### Month 3 milestone

By 2026-11-29 you should be able to:

- Explain the GPU memory hierarchy and read an Nsight Compute report for occupancy and bandwidth.
- Write a fused Triton kernel and prove with a profiler whether fusion helped.
- Type a CUDA matmul from naive to tiled to vectorised and explain each step's speedup.
- Quantize a model and state the exact accuracy cost against the throughput gain, in a table.
- Point to a leaderboard submission and a third upstream contribution.

---

## 6. Month 4: Serving at scale on Kubernetes

**2026-11-30 to 2026-12-27. Goal: run multi-replica inference on Kubernetes with KV-aware routing, dashboards, autoscaling and failure injection, and write the control-plane piece in Go.**

This is the month shaped directly around the Together AI India-remote junior posting: Go, Kubernetes operators, event-driven systems, GPU fleet automation. It is also the month that matches the most common primary requirement at every $250k+ listing, "large-scale distributed systems." You will not have a large scale. You will have the same architecture at small scale, measured, with the failure modes documented.

### What to learn

**1. Kubernetes, the parts that matter for inference**

Skip the full Kubeflow platform. Learn Kubernetes itself and the five projects the 2026 inference stacks are actually built on.

Resources:

- **Kubernetes docs** (free). [kubernetes.io/docs](https://kubernetes.io/docs/home/). v1.37. Concepts: pods, deployments, services, ConfigMaps, resource requests and limits, then custom resources and controllers.
- **Killercoda Kubernetes playground** (free). [killercoda.com](https://killercoda.com/playgrounds/scenario/kubernetes). Free one-hour clusters in the browser for the first week. Then run `kind` locally on your Mac.
- **Gateway API Inference Extension** (free). [github.com/kubernetes-sigs/gateway-api-inference-extension](https://github.com/kubernetes-sigs/gateway-api-inference-extension). v1.6.0, GA. KV-cache and load-aware routing to LLM replicas. This is the routing layer Red Hat's llm-d role asks about.
- **LeaderWorkerSet** (free). [github.com/kubernetes-sigs/lws](https://github.com/kubernetes-sigs/lws). v0.10.0. Multi-node inference "super pods."
- **Kueue** (free). [kueue.sigs.k8s.io](https://kueue.sigs.k8s.io/). v0.19.3. GPU quota and preemption queueing that every ML-on-Kubernetes stack uses.
- **llm-d** (free). [llm-d.ai](https://llm-d.ai), [github.com/llm-d/llm-d](https://github.com/llm-d/llm-d). v0.9.0, CNCF sandbox, backed by Red Hat, Google and IBM. Read the architecture and the disaggregated serving guide.
- **NVIDIA Dynamo** (free). [github.com/ai-dynamo/dynamo](https://github.com/ai-dynamo/dynamo). Disaggregated prefill and decode plus a KV router over vLLM, SGLang and TensorRT-LLM. Read the architecture docs and the KV router design.
- **NVIDIA GPU Operator** (free). [github.com/NVIDIA/gpu-operator](https://github.com/NVIDIA/gpu-operator). How GPUs get scheduled on Kubernetes at all.

**2. Go and the operator pattern**

Resources:

- **A Tour of Go and Go by Example** (free). [go.dev/tour](https://go.dev/tour/), [gobyexample.com](https://gobyexample.com/). Two weekends to working fluency if you already know TypeScript.
- **Kubebuilder book** (free). [book.kubebuilder.io](https://book.kubebuilder.io/). How to write a controller that watches a custom resource and reconciles state. This is exactly what "control planes that model state and reconcile it" means in the Together listing.
- **Temporal docs and Go SDK** (free). [docs.temporal.io](https://docs.temporal.io/). Durable workflows. Named in two 2026 Together roles. Learn the workflow, activity and retry model, then build one workflow.
- **NATS docs** (free). [docs.nats.io](https://docs.nats.io/). Lightweight event bus. Named by Together beside Kafka. Use it for the events in your project.

**3. Observability**

Resources:

- **Prometheus and Grafana docs** (free). [prometheus.io/docs](https://prometheus.io/docs/), [grafana.com/docs](https://grafana.com/docs/grafana/latest/). Prometheus 3.14, Grafana 13. Scrape vLLM's metrics endpoint, build the dashboard.
- **DCGM exporter** (free). [github.com/NVIDIA/dcgm-exporter](https://github.com/NVIDIA/dcgm-exporter). GPU utilisation, memory and temperature per pod.
- **OpenTelemetry docs** (free). [opentelemetry.io/docs](https://opentelemetry.io/docs/). Traces across gateway, router and replica. The GenAI semantic conventions moved to their own repository and are still marked "Development," so expect attribute names to change.
- **Google SRE Book and Workbook** (free online). [sre.google/books](https://sre.google/books/). Chapters on SLOs, monitoring and handling overload. You need these for month 5.

**4. DDIA continues**

Chapters on transactions, consensus, and batch and stream processing, one per Friday. By the end of this month you have read the book.

### Month 4 learning projects

The theme this month is build the naive version yourself first, then adopt the real one and understand what it adds.

- **kv-router in Go.** Before you install the Gateway API Inference Extension, write a 300-line Go reverse proxy that polls each vLLM replica's `/metrics`, picks the replica with the lowest KV-cache utilisation, and forwards the request. Compare it against round-robin on shared-prefix traffic with llm-loadgen. Then install the real extension and read its scheduler to see what your version missed, which is prefix affinity and queue depth.
- **token bucket and bounded queue, as a proxy.** A Go HTTP proxy in front of vLLM with a token-bucket rate limiter and a bounded request queue that returns 429 when full. Load it past capacity and show TTFT p99 staying flat while the unbounded version's goes vertical. This is both an interview classic and the seed of month 5's admission control.
- **mini-reconciler.** Before Kubebuilder, a 200-line Go program using client-go that reads a target from a ConfigMap, reads KV utilisation from Prometheus, and scales a Deployment up or down every 30 seconds. Then rebuild it as a proper operator with Kubebuilder and notice what the framework gives you: caching, informers, requeue, status.
- **Temporal, one workflow.** A workflow with three activities, the middle one failing randomly. Watch retries happen. Kill the worker mid-run and restart it and watch the workflow resume. Durability stops being a word.

### The month 4 project: inference-fleet

A small, real, multi-replica inference platform on Kubernetes with the same shape as the production stacks.

- **Week 1 (Nov 30 to Dec 6):** `kind` cluster on the Mac. Two CPU-only vLLM replicas of a tiny model (Qwen2.5 0.5B) behind a Kubernetes Service, so you can develop the control plane at zero GPU cost. Prometheus scraping both, Grafana showing TTFT, running requests and KV usage per replica. Go tour done.
- **Week 2 (Dec 7 to 13):** Gateway API Inference Extension installed, routing on KV-cache utilisation and prefix affinity. Your month 1 load generator drives shared-prefix traffic and you measure the TTFT difference between round-robin and KV-aware routing. This one chart is the centrepiece of the month.
- **Week 3 (Dec 14 to 20):** a Go controller, built with Kubebuilder, that watches an `InferencePool` custom resource and reconciles replica count against a KV-usage target read from Prometheus. Then a Temporal workflow that drains a replica, cordons it, restarts it and reintroduces it, with retries. Events published to NATS and logged.
- **Week 4 (Dec 21 to 27):** one rented GPU node session, about 8 hours, either a RunPod pod with Kubernetes tooling or a single-node k3s on a Vast.ai machine, to run the same stack with real GPU replicas of the 7B model. Failure injection: kill a replica under load, measure requests failed, time to recovery, and TTFT p99 during recovery. Writeup leads with the routing chart and the recovery table. Fourth upstream PR: a docs or example contribution to the Gateway API Inference Extension, llm-d or LMCache surfaced by your build.

Compute: about 12 GPU hours, about ₹1,500. Most of this month runs on your laptop.

### Month 4 milestone

By 2026-12-27 you should be able to:

- Deploy multi-replica inference on Kubernetes with dashboards from scratch in under two hours.
- Show, with a chart, how much KV-aware routing improves TTFT on shared-prefix traffic over round-robin.
- Write a Kubernetes controller in Go that reconciles a custom resource against live metrics.
- Write a durable Temporal workflow with retries and explain why durability matters for fleet operations.
- Kill a replica under load and report recovery time and error count from measurement.
- Explain disaggregated prefill and decode and when it is worth its complexity.
- Describe every requirement line in the Together India-remote junior posting from something you built.

---

## 7. Month 5: Reliability, evals and cost

**2026-12-28 to 2027-01-24. Goal: give the platform SLOs and prove it meets them under failure, build an evaluation harness for an agent workload on top of it, and publish a measured effective-cost study across providers. Also: the 2027-01-15 gate.**

This is the month that converts infrastructure into the hybrid the top postings actually screen for: serving plus cost plus latency plus reliability plus evals. It is the least glamorous month and the one that most separates you from every bootcamp graduate, because none of it can be produced without a system that already works.

### What to learn

**1. SRE for inference**

Resources:

- **Google SRE Workbook, chapters on SLO engineering and alerting** (free). [sre.google/workbook](https://sre.google/workbook/table-of-contents/). The methodology.
- **vLLM metrics design** (again). Now you use every histogram it exports to define your SLIs.
- **Kubernetes HPA and KEDA** (free). [keda.sh/docs](https://keda.sh/docs/). Autoscaling on a Prometheus metric, in your case KV-cache utilisation or queue depth rather than CPU.

Focus on:

- Defining SLIs for an inference service: TTFT p95 under 500ms, ITL p95 under 50ms, availability, and goodput.
- Error budgets and what to do when you burn one.
- Overload handling: admission control, queue limits, shedding, and why unbounded queues make TTFT catastrophic.
- Capacity math: tokens per second per GPU, cost per million tokens at your real hourly price, and break-even utilisation.

**2. Evals for agent workloads**

Resources:

- **Anthropic, Demystifying evals for AI agents** (free). [anthropic.com/engineering/demystifying-evals-for-ai-agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents). January 2026. The best single read on agent evaluation. Then, from the same engineering blog: Building effective agents, Writing tools for agents, Effective context engineering, and Quantifying infrastructure noise in agentic coding evals.
- **Hamel Husain, Evals FAQ** (free). [hamel.dev/blog/posts/evals-faq](https://hamel.dev/blog/posts/evals-faq/). Updated September 2026. The practitioner reference. Skip the $4,200 course; the FAQ covers it.
- **Inspect, UK AI Security Institute** (free, MIT). [inspect.aisi.org.uk](https://inspect.aisi.org.uk/). The most infrastructure-serious open eval framework, with sandboxed tool execution. Your primary harness.
- **promptfoo** (free, MIT). [github.com/promptfoo/promptfoo](https://github.com/promptfoo/promptfoo). YAML evals in CI. Use it for the regression suite.
- **Langfuse** (free, MIT core). [github.com/langfuse/langfuse](https://github.com/langfuse/langfuse). Self-hosted traces of every agent run. Part of ClickHouse since January 2026, still self-hostable.

Focus on:

- Task-level pass rates with confidence intervals, not vibes.
- Separating model failures from infrastructure failures, which the Anthropic noise post shows is the hard part.
- Cost and latency per task as first-class eval metrics beside accuracy.

**3. Effective cost across providers**

Your old venture idea returns here as a measurement study. The 566-upvote Reddit thread that validated it was about provider cache-hit inconsistency wrecking cost predictability. That is a benchmarking problem, and you now know how to benchmark.

Resources:

- **Artificial Analysis** (free). [artificialanalysis.ai](https://artificialanalysis.ai/). Speed and price per provider, updated daily. Your baseline for list prices.
- **Provider prompt-caching docs** (free). Anthropic, OpenAI, Google, Together, Fireworks. Each defines cache hits, TTL and pricing differently, which is the whole point.

**4. Speculative decoding**

- **EAGLE-3** (free). [arXiv 2503.01840](https://arxiv.org/abs/2503.01840). What vLLM and SGLang ship. Read the method, then enable it in vLLM and measure.

### Month 5 learning projects

- **speculative decoding from scratch.** In PyTorch, with a small draft model and a larger target model from Hugging Face: draft k tokens, verify them in one target forward pass, accept the prefix that matches under rejection sampling, resample the first miss. Measure acceptance rate and wall-clock speedup at k of 2, 4 and 8. Then enable EAGLE-3 in vLLM and understand what a trained draft head adds over a plain small model. This is the second most valuable learning project of the year after mini-vllm.
- **burn-rate alerts on synthetic data.** Generate a week of synthetic TTFT samples with a few incidents injected, implement the SRE Workbook's multi-window multi-burn-rate alerting, and count true and false alerts. Tune the windows. You will never again configure an alert threshold by feel.
- **evals in fifty lines, then Inspect.** Before using Inspect, write the smallest possible harness: run each of ten tasks five times against your endpoint, compute pass rate with a Wilson confidence interval, print a table. Then port it to Inspect and see what a real framework gives you: sandboxing, scorers, logging, parallelism.
- **attention variants and the KV bill.** Implement multi-head, grouped-query and multi-query attention in your nanoGPT and compute the KV bytes per token for each. Then read the MLA section of the DeepSeek-V2 paper and compute its KV size. One table, four rows, and you understand why every 2025 and 2026 model changed its attention.

### The month 5 project: inference-fleet, part two, plus the effective-cost index

- **Week 1 (Dec 28 to Jan 3):** SLO document for inference-fleet committed. KEDA autoscaling on KV utilisation. Load test that pushes past capacity and shows admission control keeping TTFT p95 inside the SLO while shedding excess. Chart of TTFT p95 with and without admission control.
- **Week 2 (Jan 4 to 10):** Inspect harness running a small tool-using agent task suite (twenty tasks, three trials each) against your own vLLM endpoint and against one hosted provider. Report pass rate with intervals, cost per task, latency per task. Langfuse traces for every run.
- **Week 3 (Jan 11 to 17):** the effective-cost probe. A harness that sends identical shared-prefix workloads to four providers, measures actual cache-hit rate and effective cost per million tokens against list price, three times a day for a week. Published as a page with the numbers. This is a real contribution nobody else has made public, and it is the thing from the old venture plan worth keeping. **January 15 is the gate: read section 10.**
- **Week 4 (Jan 18 to 24):** speculative decoding with EAGLE-3 enabled on inference-fleet, acceptance rate and speedup measured at three batch sizes. Combined writeup for the month. Fifth upstream PR, to Inspect, promptfoo, vLLM or llm-d.

Compute: about 30 GPU hours, about ₹2,000, plus about ₹2,000 of hosted-provider API spend for the cost probe.

### Month 5 milestone

By 2027-01-24 you should be able to:

- Write an SLO document for an inference service and show measured compliance under overload.
- Explain admission control, autoscaling on KV utilisation, and error budgets from your own charts.
- Run an agent eval suite and report pass rate, cost and latency per task with intervals.
- Show a published effective-cost comparison across four providers with measured cache-hit rates.
- Measure speculative decoding acceptance rate and speedup and say when it is not worth it.
- Point to five upstream contributions across at least three projects.

---

## 8. Month 6: Portfolio, visibility, and the first fifty applications

**2027-01-25 to 2027-02-28. Goal: turn five months of shipped work into a record that gets replies, put yourself in front of the communities that hire, and start applying to non-Indian companies with the setup to accept an offer.**

Everything before this was engineering. This month is distribution, and you are good at distribution because you have shipped web products. Treat your own record as the product.

### 1. The portfolio rewrite

Take the four repos and rewrite every README to the same structure:

- A 60-second screen recording or GIF at the top showing the thing working.
- The headline table of measured numbers, before any prose.
- An architecture diagram.
- "What broke and how I fixed it," with at least three entries each, specific enough that an interviewer can ask a follow-up.
- "What I would do next," honest about limits.

Recruiters in this field say the same things: logged metrics and a commit history that shows iterative debugging rank highest, real deployment evidence beats simulation, upstream contributions to the packages employers depend on rank above everything except shipped systems, and tutorial certificates rank near zero. Red flags they name: projects that cannot survive three follow-up questions, and a pure deep-learning background with no systems understanding.

Practice task: have someone interrogate you about your own code for twenty minutes. Why this gain, why this backend, what happens when the replica dies mid-prefill, what did you try first. If you cannot go three levels deep on any line, that repo is not ready.

### 2. Visibility that compounds

- **Host the first vLLM or LMCache meetup in Chennai.** vLLM lists no India meetup anywhere. Thirty people in a borrowed office, two talks, one of them yours on kv-arena. Post the recording. This single act puts you on the maintainers' radar more than fifty PRs.
- **One talk proposal** to an online venue: a vLLM office hours slot, a GPU MODE lightning talk, or a PyTorch community talk on your quantization table.
- **Weekly posts on X**, one per shipped result, each with a chart. You have five months of charts.
- **The UK Global Talent evidence folder.** Start it now even if you never apply. Talks, merged PRs with maintainer comments, the writeups, and press or podcast mentions. The Promise route needs two of four criteria and no employer, and building the folder makes you do the things that count.

### 3. The setup to accept a non-Indian offer

- Register as a sole proprietor and understand section 44ADA: 50% of gross receipts up to ₹75 lakh is deemed income, export of services is zero-rated for GST with a Letter of Undertaking, and W-8BEN plus the India-US tax treaty means no US withholding. A contractor at ₹30 lakh gross takes home more than an employee at the same figure. Above ₹75 lakh you need an LLP, which is a 2028 problem.
- Understand that contractors get no equity, no experience letter, and no notice period protection. Ask for a fixed monthly retainer, not hourly.
- Bank account that receives USD without a 3% spread: Wise, or a domestic bank's forex account. Compare.

### 4. Interview preparation

Robotics has its interview shape and so does this. Expect:

- A systems design round scoped to inference: "design a multi-tenant LLM serving platform with an SLO," "design KV-cache sharing across replicas," "design a benchmark that a competitor could not game." You have built all three.
- A profiling or debugging exercise: here is a slow kernel or a serving trace, find the problem. Nsight and py-spy fluency is what they are testing.
- Coding in Python and one of C++ or Go, usually concurrency-flavoured: implement a rate limiter, a token bucket, a bounded queue with backpressure, an LRU cache with TTL.
- A deep conversation about a specific past failure and how you diagnosed it. Your "what broke" sections are the preparation.

Resources:

- **Glassdoor, machine learning infrastructure engineer interview questions** (free). Read fifty real ones.
- **Your own repos.** Every question they ask maps to something you measured.

### Month 6 learning projects

Lighter, because this month is distribution. These are interview preparation with code.

- **the kata set, timed.** An LRU cache with TTL, a token bucket, a bounded blocking queue with backpressure, and a top-k over a stream, each in Python and in Go or C++, each under 45 minutes from a blank file. Repeat until the times hold. These are the coding questions inference teams actually ask.
- **three one-page designs.** Written, with a diagram each: a multi-tenant LLM serving platform with per-tenant SLOs, KV-cache sharing across replicas, and a public inference benchmark a vendor could not game. You have built pieces of all three, so each page is a summary of measured experience rather than a guess. Bring them to interviews.
- **learning-lab README.** One index page across all the learning projects, each with its one number and one sentence on what it taught you. This is the page you send when someone asks "how did you learn this."

### 5. The first fifty applications

Non-Indian employers only, in this priority:

1. **Together AI, Junior SWE Inference and Compute Infrastructure, remote India.** Apply the day the portfolio rewrite is done. Reference inference-fleet directly against each requirement line.
2. **US seed and Series A AI-infrastructure startups without an India entity**, found via the LinkedIn remote filter and Wellfound with "worldwide" location. The Blind data point of $110k fixed at five years came from exactly this filter. At your experience the band is $30k to $60k, and the point is the first non-Indian line on the record.
3. **Remote-first companies with India-adjusted USD pay**: Coinbase, Atlassian, GitLab, Automattic, HashiCorp, Weights and Biases, Hugging Face. Infra and platform roles, not ML research.
4. **Netherlands and UAE employers** for the relocation door: any Amsterdam or Dubai infra role above the HSM threshold.
5. **Red Hat, NVIDIA, Cerebras** for any remote or relocation-eligible role, with your merged PRs as the opener. Not their India offices, per your constraint, unless you change your mind about staging.

Fifty applications, each with a two-line note pointing at the one repo that matches the posting. Track them in a sheet. Expect a 5% reply rate and a 1% offer rate at this stage, which is two to three conversations and possibly one offer. That is the March 2027 checkpoint.

### Month 6 milestone

By 2027-02-28 you should have:

- Four public repos with video, numbers, diagrams and failure writeups, each surviving three follow-ups.
- One meetup hosted or one talk given, recorded.
- Five or more merged upstream contributions across at least three inference projects.
- A contract-ready tax and banking setup.
- Fifty applications sent to non-Indian employers, tracked.
- A UK Global Talent evidence folder with its first entries.

---

## 9. Hardware and compute, in rupees

You have a Mac. You do not buy a GPU this year. Here is why, with the numbers.

### Rental prices, verified 2026-09-04, at ₹94.6 per dollar

| Provider | RTX 4090 24GB | A100 80GB | H100 80GB | Notes |
|---|---|---|---|---|
| RunPod community | $0.34/hr (₹32) | $1.19/hr (₹113) | $1.99/hr PCIe (₹188) | Prepaid from $10 with an Indian Visa or Mastercard, which sidesteps the RBI recurring-payment problem. Your default. |
| RunPod secure | $0.74/hr (₹70) | $1.39/hr | $2.89/hr | When you need it not to disappear mid-run. |
| Vast.ai | from $0.13/hr, median $0.37 | median $1.03 | from $1.33, median $2.39 | Marketplace. "From" prices are interruptible hosts. Good for cheap long benchmark runs. |
| Modal | — | ~$2.50/hr | ~$3.95/hr | $30 a month free credits on the starter tier. Card required. Use the free credit for month 5's eval runs. |
| Lambda | — | $2.79/hr | $3.99/hr | Reliable, pricier. |
| E2E Networks (India, INR) | — | ₹189/hr | ₹362/hr, spot ₹70/hr | INR billing, GST extra. The spot H100 at ₹70 is the cheapest H100 in this table when it is available. |
| Yotta Shakti (India, INR) | — | — | ₹356/hr | INR only. |

Free tiers worth stacking: Kaggle gives two T4s or a P100 for 12-hour sessions, fine for quantization and eval runs. Colab's free tier exists and Pro is $11.79 a month, but monthly USD subscriptions are where Indian cards get declined under RBI e-mandate rules, so prefer prepaid top-ups. Lightning AI gives about 80 interruptible GPU hours on signup. Hugging Face PRO at $9 a month gives 40 minutes a day of ZeroGPU on a Blackwell card. Google Cloud's $300 trial does not include GPUs.

### Your monthly budget against the plan

| Month | GPU hours | Approximate cost |
|---|---|---|
| 1 | 25 on 4090 | ₹800 |
| 2 | 30 on 4090 plus 6 on H100 | ₹2,500 |
| 3 | 40 on 4090 plus 2 on H100 | ₹1,900 |
| 4 | 12 on GPU node | ₹1,500 |
| 5 | 30 on 4090 plus provider API spend | ₹4,000 |
| 6 | Reruns for videos | ₹800 |

Total about ₹11,500 over six months, which is less than a single month of the robotics roadmap's hardware.

### If you are tempted to buy

A new RTX 5090 is ₹5.75 to 6.6 lakh in India, 90% to 200% over MSRP. A new 4090 is effectively unavailable. Used 4090s on OLX are ₹2.4 to 2.6 lakh, and the sub-₹1 lakh listings are scam patterns. The only sane local purchase is a same-city used RTX 3090 24GB at ₹40k to 65k, and a ₹60k 3090 equals about 1,875 hours of RunPod community 4090 time. You will not use 1,875 hours in six months. Rent.

Your Mac is genuinely useful for llama.cpp with Metal and for MLX experiments, and it runs the entire month 4 control plane with CPU-only replicas. It cannot run CUDA, Nsight or Triton, so every kernel session is a rented session.

---

## 10. Parked, with dates

Things that were considered and deliberately set aside. Each has a date on which you may reopen it and not before.

| Item | Why parked | Reopen on | Condition to reopen |
|---|---|---|---|
| **Robotics roadmap** | Three of six months are hardware with no transfer to the target. Least remote-friendly field. India median below your current salary. | 2027-01-15 | If the infra track is on schedule and you want a specialisation expression, the software half (ROS 2 as a distributed system, VLA inference on Jetson-class hardware) becomes a month 7 to 9 elective. |
| **GATE and M.Tech, Plan B** | Settled 2026-07-22 as gated Plan B. | 2027-01-15 | Evaluate with five months of evidence in hand. If fewer than three merged PRs and no shipped measured project exist by then, the throttle-2 path has not worked and Plan B is live. |
| **Venture SaaS track** | Thirteen hours a week does not fund two tracks. Nothing shipped in five days of the dual plan. | 2027-03-01 | Reopen only if the effective-cost index from month 5 has strangers using it. Then it is a product with evidence, not an idea. |
| **Rust** | The inference stacks you contribute to are Python, C++ and CUDA. Go is what the India-remote listings ask for. | 2027-03-01 | If you target candle or mistral.rs, or an employer names Rust, take four weeks then. |
| **Distributed training** | Absent from inference postings. | 2027-06-01 | Literacy only, via the Ultra-Scale Playbook and torchtitan, when a role asks. |
| **Indian offices of US companies as an L-1B staging move** | You said no Indian jobs. | Your call | It remains the single most reliable route to US pay from where you stand. NVIDIA India IC3 pays about $65k and makes you L-1B eligible after one year. If March 2027 produces no non-Indian offer, reconsider. |

---

## 11. Beyond month 6: the shape of 2027 and 2028

This is a sketch, not a plan. It exists so the six months above point somewhere.

**Months 7 to 12, March to August 2027.** You are either on a remote contract or still applying. Either way: become a recognised contributor to one project rather than a drive-by to five. Pick vLLM, SGLang, LMCache or llm-d based on where your PRs landed most easily. Take on a tracked issue that spans weeks. Attend office hours until they know your name. Second Chennai meetup. Apply to the UK Global Talent Promise route in the autumn if the evidence folder has two criteria covered.

**Months 13 to 24, September 2027 to August 2028.** Target the September 2028 checkpoint bands: $80k to $150k India-remote or a relocation. The Netherlands HSM opens with any offer above about €52k. If you are on a remote contract with a US startup, ask about a US or EU transfer. If a relocation offer appears at $75k to $110k in Europe, understand that it is a stepping stone to US pay, not the destination, and that living costs eat much of the difference from a $60k India contract.

**2029 to 2031.** The $300k conversation. From a US or London or Dubai seat, at senior level, with a five-year public record in inference systems. The evidence says this is when it becomes possible, and the evidence says almost nobody who starts where you are gets there, because almost nobody ships for five years in public. That is the whole bet.

---

## 12. The Sunday check

Copy this into `WEEKLY.md` every Sunday. No coach reads it. You do.

```
## Week of YYYY-MM-DD

Shipped: <link to commit, PR, or writeup>
Measured: <one number from this week, with units>
Broke: <one thing that failed and what you learned>
Next ship: <one sentence, due next Sunday>
```

If the first line has no link, the week did not ship, and Monday's first task is the smallest commit that fixes that.

---

## Verification notes

All prices, versions and job requirements were checked on 2026-09-04. Things that could not be verified and are therefore stated cautiously or omitted: Colab pricing in INR, Vast.ai's accepted payment methods, NVIDIA DLI free course availability (site down), PMPP 5th edition price, Dynamo's latest stable tag, any named case of an India-based junior reaching $200k remote via inference open source. Resources deliberately excluded because they are stale: Hugging Face Text Generation Inference (archived March 2026), the Open LLM Leaderboard (retired March 2025), PMPP 4th edition (superseded), PyBullet, Kubeflow as a full platform, and all ROS 1 material.
