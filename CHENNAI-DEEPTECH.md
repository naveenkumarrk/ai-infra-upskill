# Chennai deep-tech: who to contact, what to offer, and whether weekends are realistic

**Compiled 2026-09-11. Sources: a logged-in LinkedIn pass across eleven companies, plus company sites, LinkedIn company pages, Wikipedia and Google News, all read on 2026-09-11.**

The idea: spend weekends contributing software to a Chennai deep-tech company, most of them IIT Madras linked, in space, robotics, defence, drones or mobility. This document is the map, the eligibility scoring, the named people, and the honest read on whether it works.

Everything here is a public business channel: company emails from company websites, public LinkedIn profiles, careers pages. No personal phone numbers or private addresses were collected, and none are needed.

---

## 0. The honest read before you send anything

Three things you should weigh before spending a Saturday on this.

**Weekend arrangements at hardware companies are rare, and the reason is structural.** These companies build physical things on a lab floor. Their bottleneck is usually hardware, test slots and certification, not a missing web developer. The work that genuinely can be done remotely on a Saturday is the software around the hardware: dashboards, telemetry views, inspection-report portals, internal tooling, simulation glue, data pipelines, CI. That surface is real at maybe five of the eleven companies below, and non-existent at the rest.

**Check your own employment contract first.** Moonlighting in India is a contractual question, not a legal one. Look for three clauses in your firmly.ai agreement: exclusivity of service, intellectual property assignment, and non-compete. IP assignment is the one that bites, because a broadly worded clause can claim code you write on a Sunday. The clean paths, in order of safety: contribute to a company's public open-source repo under your own name; or take a small written contract with a scope that is obviously outside your employer's business; or ask your employer for written consent, which small startups often give. Do not run an undisclosed paid engagement that overlaps your employer's domain.

**Defence work has a hard gate.** Big Bang Boom, Vinveli and parts of Dhaksha and Zuppa build for the armed forces. Those programs carry vendor rules, NDAs and sometimes clearance requirements that make a casual outside contributor a compliance problem rather than a help. If you approach them, aim explicitly at non-classified internal tooling and say so in the first message.

**What this is actually for.** Be clear with yourself. This is not the $300k path, which is section 0 of the roadmap and runs through public inference-infrastructure work. This is a way to get real systems experience, a local network in the IIT Madras ecosystem, and possibly a reference. Treat it as a supplement that costs at most one weekend day, and keep the kv-arena and upstream-PR work as the priority. If this starts eating the roadmap, it has failed.

---

## 1. The eligibility rubric

Score each company 0, 1 or 2 on eight questions. Maximum 16. Anything at 11 or above is worth a message this month.

| # | Question | 2 points | 1 point | 0 points |
|---|---|---|---|---|
| 1 | Is there a real software team? | Several named software or AI engineers | One or two | None visible |
| 2 | Is the software surface non-safety-critical? | Dashboards, portals, tooling, data | Mixed | Flight or control critical only |
| 3 | Part-time, intern or contractor precedent? | Contractor or remote intern on staff | Interns on site | None found |
| 4 | Team under 50 people? | Under 50 | 50 to 200 | Over 200 |
| 5 | Hiring software right now? | Open software role posted | Hiring generally | Not hiring |
| 6 | Work possible without lab presence? | Fully remote-able | Partly | Needs hardware access |
| 7 | No clearance or defence gate? | Civilian only | Mixed portfolio | Defence core |
| 8 | Reachable founder or engineering lead? | Named, active, public profile | Named only | Opaque |

---

## 2. The eleven companies, scored

| Rank | Company | Sector | Score | Why |
|---|---|---|---|---|
| 1 | **Detect Technologies** | Industrial AI vision, safety and compliance | 15 | Large distributed AI team, staff working remotely from Delhi, Nagpur and Hyderabad, an engineer whose title is literally distributed real-time inference, and a Google Summer of Code alumnus on the team. Civilian. |
| 2 | **TuTr Hyperloop** | Maglev and linear-motor freight | 14 | Hiring a senior software engineer in Chennai right now. Has an engineer building real-time perception and telemetry. Small team, IIT Madras Research Park, hard customer deadlines in October 2026 and June 2027. |
| 3 | **Solinas Integrity** | Pipeline inspection robots | 14 | Small React and Java software team, a computer-vision engineer, a past software intern and a past remote operations intern. Mission-driven, civilian, approachable staff. |
| 4 | **Planys Technologies** | Underwater inspection ROVs | 13 | Already engages a software consultant, has a software engineer on staff, IIT Madras CTO, and inspection-data post-processing is exactly weekend-shaped work. |
| 5 | **The ePlane Company** | eVTOL air taxi | 12 | Has an AI, computer-vision and digital-twin team using NVIDIA Omniverse and Isaac Sim, plus a documented intern-to-hire path. Certification pressure means the flight side is closed, but simulation and digitalisation are not. |
| 6 | **Agnikul Cosmos** | Orbital launch vehicles | 11 | Runs an internal automation and ERP team separate from flight software, currently lists an ERPNext developer role, and has a software automation intern on staff. Bigger and more formal than the others. |
| 7 | **Big Bang Boom Solutions** | Defence, anti-drone, AI | 10 | Genuine software and AI team with several engineers working remotely from other Tamil Nadu cities. Marked down only for the defence gate. |
| 8 | **Garuda Aerospace** | Agricultural and industrial drones | 9 | Has an AI and ML department and, notably, a college professor holding a research fellowship there while employed elsewhere, which is the exact arrangement you want. But it is large and operations-heavy. |
| 9 | **Mindgrove Technologies** | RISC-V system-on-chip | 9 | Mostly VLSI, RTL and verification. The software surface is the software development kit, toolchain and developer portal. Interesting for the hardware side of your curiosity, off-centre for your web and infrastructure edge. |
| 10 | **Zuppa Geo Navigation** | Indigenous drone autopilot | 6 | Autopilot firmware is not weekend work and no software team is visible. Only route would be a fleet or telemetry web layer. |
| 11 | **Dhaksha Unmanned Systems** | Drone manufacturing | 5 | Production, quality and pilots. No visible software team. |

Also in the ecosystem but excluded, with reasons: **GalaxEye Space** is IIT Madras incubated but its operational headquarters moved to Bengaluru and only its registered office is in Chennai, so it is remote-only for you, though its stack is the most interesting on this list. **Space Kidz India** is a two-to-ten person education non-profit, so the offer there would be volunteering with students, not engineering. **Space Zone India** runs fee-paying student internships, which is the wrong direction of money. **Aerostrovilos** has a lapsed website domain and its status is uncertain after a corporate stake purchase, so verify it exists before spending time.

---

## 3. Who to contact at each, and why that person

Message one person per company. Pick the engineering owner, not the chief executive, unless the company is tiny. Chief executives at Agnikul and Garuda get hundreds of messages a week; the person who owns the internal tooling gets almost none.

### Detect Technologies
- **First contact: Samjith Raj CP, Lead AI Engineering.** Profile: linkedin.com/in/samjith-raj-cp-270b2339. His own headline mentions generative AI, deep learning and agentic AI, so he is the person whose backlog you would be shortening.
- Backup: Rohithkumar Ravi, Senior Manager Applications, linkedin.com/in/rohithkumar-ravi, who owns the application layer.
- Peer worth following first: Sankalp Singh, Senior AI Software Engineer, computer vision and distributed real-time inference, working remotely, linkedin.com/in/sankalp-s-singh. His work is the closest thing in Chennai to your own target skill set.
- Culture signal to use: Dhanus SL on the team did Google Summer of Code with OpenWISP, so open-source contribution is understood there.

### TuTr Hyperloop
- **First contact: Karthik Sundaram, Head of Digital Solutions**, named on tutr.tech/about. He owns software.
- Peer and warm route: Sirish S., AI/ML and systems engineer, building real-time perception and telemetry, linkedin.com/in/caffeowl. His stack is PyTorch, AWS, Go and Rust with edge AI, which overlaps yours.
- Formal route: they are advertising a senior software engineer role in Chennai using PHP, Laravel, Node.js, Python and the usual databases. Apply at careers@tutr.tech and say plainly you are not applying full-time but want to contribute weekends on a scoped piece.
- General contact: info@tutr.tech. Office: IIT Madras Research Park, Kanagam Road, Taramani.

### Solinas Integrity
- **First contact: Pranav Guhan M, Communications and Partnerships**, linkedin.com/in/pranav-guhan-m-929485185. Partnerships people reply, and their job is to route you to the right person.
- Engineering: Rajeshkanth M, software engineer, React, Java, linkedin.com/in/rajeshkanth4051.
- Founder's office: Nitish J, linkedin.com/in/nitish-j-0b8a11191.
- Precedent to cite: they have had a software engineering intern and a remote technical operations intern.

### Planys Technologies
- **First contact: Vineet Upadhyay, Co-founder and CTO**, linkedin.com/in/vineetupadhyay25. IIT Madras, Forbes Under 30 Asia, and at a company this size the CTO still reads messages.
- Precedent to cite: they already work with a software engineering consultant, Akshaya Ramaswamy, linkedin.com/in/akshaya-ramaswamy-01254896, so an outside contributor is not a novel idea there.

### The ePlane Company
- **First contact: Shravan Krishnan, Associate Director for Future Programs, Intelligence and Digitalisation**, linkedin.com/in/shravan-krishnan. The word digitalisation in a job title means internal software nobody has time to build.
- Alternative gatekeeper: Nithyashree S., Associate Vice President for New Initiatives and Chief of Staff, linkedin.com/in/inbox-nithya. Chief-of-staff roles exist to handle exactly this kind of non-standard proposal.
- Interesting peer: Roshan Akthar, Aircraft Digital Twin Engineer working in NVIDIA Omniverse and Isaac Sim, linkedin.com/in/roshan-akthar26.
- Founder: Prof. Satya Chakravarthy, linkedin.com/in/satya-chakravarthy-51326241. Note he is also a co-founder of Agnikul and TuTr, so one good impression travels across three companies.

### Agnikul Cosmos
- **First contact: Yashawanth S M, Product Lead**, linkedin.com/in/yashawanth-s-m, whose headline is automating operations and building AI-driven enterprise systems. That is the non-flight software surface.
- Peer: Senthilnathan Selvarajan, full-stack developer automating enterprise operations, linkedin.com/in/senthilnathanselvarajan.
- Formal route: humancapital@agnikul.in, which their careers page names for applications. General: curious@agnikul.in. They currently list a Mission Design Software Developer and an ERPNext developer.
- Do not lead with flight software. Sixty-eight people there match "software" and the flight side is a closed, certified world.

### Big Bang Boom Solutions
- **First contact: Venkatakrishnan Venkatesan, Lead Software Engineer**, linkedin.com/in/venkatakrishnan-venkatesan-8a5234a4, based in Tiruchirappalli, which itself proves they employ software people away from the office.
- Peer: Ragul TN, full-stack developer working on agentic and real-time systems from Nagercoil, linkedin.com/in/ragulsid, who is a Google Developer facilitator and therefore community-minded.
- Say in the first message that you understand defence programs have access restrictions and you are offering to work only on internal, non-classified tooling.

### Garuda Aerospace
- The angle here is the **research fellowship**, not a job. A professor at KPR Institute holds one at Garuda while employed elsewhere, linkedin.com/in/vignesh-cj-43a72967. Ask what their fellowship or research-associate programme looks like for a working engineer.
- They also take AI and ML research interns.

### Mindgrove Technologies
- **First contact: Sharan Jagathrakshakan, Co-founder and CTO**, linkedin.com/in/sharanj.
- Realistic offer: developer experience. Their software development kit documentation, a board bring-up guide, a developer portal. Small, well-scoped, and genuinely useful to a chip company whose engineers are all in RTL and verification.

---

## 4. What to actually offer

Do not offer "help" in the abstract. Offer a specific artifact you will deliver in two weekends, free, with no obligation, and name what you will need from them. This is the difference between a message that gets ignored and one that gets a reply.

Good offers by company type:

| Company type | The offer |
|---|---|
| Inspection robotics: Planys, Solinas, Detect | An inspection-report web viewer, or a dashboard that turns raw run data into a client-ready report. Both companies deliver reports to industrial clients and both hate making them. |
| Telemetry-heavy: TuTr, Agnikul, Zuppa | A live telemetry dashboard, or a replay tool for recorded test runs so engineers can scrub through a run in a browser. |
| AI-vision: Detect, ePlane, Big Bang Boom | A benchmark harness that measures model latency, throughput and cost per stream on their edge hardware, with a results page. This is your kv-arena skill pointed at their problem and almost nobody offers it. |
| Chip: Mindgrove | A documentation site and getting-started guide for their software development kit, built properly. |

Terms to propose, in this order: unpaid for the first deliverable so there is no contractual entanglement while you check your employment agreement, then a small fixed monthly contract if it continues. Ask to keep a public write-up of what you built, with anything sensitive removed. That write-up is the point. Never accept an open-ended unpaid trial with no defined deliverable; two weekends and a named artifact, then a decision.

---

## 5. Message templates

Keep them under 120 words. Lead with the thing you built, not with wanting.

**Template A, engineering lead, cold**

> Hi [name], I'm a software engineer in Chennai. I build web and infrastructure tooling, and I benchmark LLM inference systems in my own time, repo here: [link].
>
> I have Saturdays free and I'd like to spend them on something physical rather than another side project. Concretely: I'd build you [one specific artifact] over two weekends, unpaid, no obligation. If it's useful we talk about continuing, if not you've lost nothing but a design conversation.
>
> I'd need [the one input, e.g. a sample data file and thirty minutes of your time]. Worth a fifteen-minute call?

**Template B, partnerships or chief of staff**

> Hi [name], I'm a Chennai-based software engineer, TypeScript and Next.js plus infrastructure work.
>
> I'm looking for a weekend engineering contribution at a company building physical things, and [company] is top of my list because [one specific, true reason: the port pilot, the lunar mission, the sewer-robot deployment]. I'm not asking for a job. I'd build one scoped piece for free over two weekends, e.g. [artifact].
>
> Who on the engineering side would be the right person to ask?

**Template C, the fellowship ask, for Garuda and Agnikul**

> Hi [name], I noticed [company] works with research fellows and interns alongside full-time staff. I'm a working software engineer in Chennai, weekends free, with a portfolio in web tooling and LLM inference benchmarking: [link].
>
> Is there a fellowship or research-associate arrangement that fits someone employed full-time elsewhere? I'd be contributing on [area], and I'm happy to start with an unpaid scoped deliverable.

---

## 6. The sequence

Do not send eleven messages at once. You will burn the list with a template that has not been tested.

- **Week 1.** Send to the top three only: Detect, TuTr, Solinas. One message each, to the named person, each customised with a real detail about their work. Track replies in a simple sheet.
- **Week 2.** Read what came back. Fix the message. Send to Planys, ePlane and Agnikul.
- **Week 3.** Big Bang Boom, Garuda, Mindgrove.
- **In parallel, the highest-yield move that is not a message at all:** go to IIT Madras Research Park in person. Agnikul, TuTr, Solinas, Mindgrove and ePlane are all in or around that building. Attend one public event there and you will meet more of these people in an evening than a month of cold messages will reach.
- **Expect:** roughly one reply in three for a well-targeted message with a portfolio link, and at most one of those turning into real work. That is a normal outcome, not a failure.

---

## 7. What is still unverified

Be honest about the gaps in this document when you act on it.

- The feasibility research on moonlighting law, defence contractor rules and documented weekend-contributor precedents was cut short. Before signing anything, read your own employment contract and, for defence companies, ask them directly what an outside contributor is permitted to touch.
- Company headcounts, funding and locations come from LinkedIn and press, not from the companies themselves. Verify in the conversation.
- Two funding figures are medium confidence: Agnikul's reported November 2025 round and GalaxEye's March 2026 extension, both from news headlines rather than full articles.
- Aerostrovilos may be dormant. Its website domain now redirects elsewhere.
- Founder LinkedIn URLs for TuTr's leadership were not surfaced in the search pass. Find them through the company's People tab when you write.
