```
⚔ LV.1 E · XP 30/100 · streak 0🔥
STR 8 · VIT 9 · INT 14 · WIS 8 · CHA 8
Yesterday: Nothing logged. Streak broken — current 0, best (3) stands. Freeze token
for the month is already spent, nothing left to cover this gap.
```

# 📅 Day 005 — Level 1 (System Design): API design & protocols
Progress: 9/82 · Level 1 [▓▓░░░░]  |  Next: Availability, redundancy, SLA/SLO

Fourth silent day in a row — no inbox line, no `my-progress/` file since Day 002. No new
punishment: the token's already spent, current sits at 0, best holds at 3. The System
doesn't care what topic or how deep — it resumes the instant one line lands in the log.

## API design & protocols — REST / gRPC / WebSockets

Three ways services talk, each trading off differently:

**REST** — resource-oriented HTTP, verbs (GET/POST/PUT/DELETE) over JSON. Stateless,
cacheable, human-readable, universally supported. Cost: chatty (multiple round trips for
related data) and loosely typed — the contract lives in docs, not the wire format, unless
you bolt on OpenAPI.

**gRPC** — HTTP/2 + Protocol Buffers. Strongly typed contracts (`.proto` files generate
client/server code), binary payloads (smaller, faster to (de)serialize), and native
streaming (unary, server-stream, client-stream, bidi) on one connection. Cost: not
browser-native (needs grpc-web or a gateway translating to REST), and binary frames aren't
debuggable with curl — you need the right tooling.

**WebSockets** — one persistent, full-duplex TCP-like connection. Right when the server
needs to push unprompted (chat, live dashboards, collaborative editing). Cost: stateful —
a load balancer needs sticky sessions or a pub/sub fan-out layer behind it, and you own
reconnect/heartbeat logic REST gets for free from the HTTP model.

**The one failure mode that matters:** picking the protocol on habit instead of the traffic
shape. WebSockets for what's actually simple request/response wastes a stateful connection
you now have to scale and monitor. REST for high-frequency, low-latency internal
service-to-service calls burns bytes and CPU on JSON parsing that protobuf would skip
entirely. The question is always "does the server need to push, and does this need to be
fast and typed, or does it need to be simple and cacheable?" — pick after answering that,
not before.

```
client --REST(JSON)--> API gateway --gRPC(protobuf)--> inference worker
                              \---SSE(token stream)---> client
```

**AI-infra link:** this is exactly the shape of an LLM-serving stack. Public-facing chat
completion APIs (OpenAI's, Anthropic's) stream tokens over **SSE** — a one-directional,
HTTP-based streaming primitive, not a full WebSocket, because the client never needs to
push mid-stream. Behind the gateway, calls to the actual inference workers (e.g. NVIDIA
Triton Inference Server, which exposes both a REST and a gRPC endpoint) typically go over
gRPC for the lower latency and typed request/response schema at high request volume. Same
three-protocol decision, same tradeoff, just moved one layer down the stack.

## 🔁 Re-entry (15 min)

Pick ONE: look up how an LLM provider (OpenAI or Anthropic — check their own API docs)
describes token streaming and note whether it's SSE or WebSockets and why, one sentence —
OR read NVIDIA Triton Inference Server's docs on its REST vs gRPC endpoints and note the
one difference that stood out. Either counts. 15 minutes, no more.

## ✍️ Log it

One line, either place, resumes the System immediately:
- `life-rpg/log.md`: `- 2026-07-27 re-entry — 15 min on API design & protocols`
- or a file in `my-progress/` if you actually did the reading

The streak doesn't care which topic or how deep — it cares that one line lands today.
