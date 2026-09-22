# Trần Ngọc Tiến

Full-stack developer, backend-leaning. I build production systems — payment infrastructure,
multi-tenant SaaS, and AI/agent products.

Currently at **IMbrace** (Hong Kong) on an enterprise AI platform, where I built the company's
payment service (gateway-agnostic, Stripe on AWS Lambda + DynamoDB, exactly-once webhook
processing), an Ed25519 offline licensing system across four microservices, and workflow
automation plus AI-agent tooling — full-stack.

Most of my professional work lives in private company repositories. What is
public here is clean-room, from-scratch: one product and the four libraries
extracted from it, built so the reasoning is public even where the code cannot be.

## Selected public work

One product and the four libraries extracted from it. Every repo has a README
that explains the design decisions, a test suite that fails if a guarantee is
removed, and CI that runs it.

**[digital-marketplace](https://github.com/tientran1234/digital-marketplace)** —
A marketplace for digital products where every listing comes with an assistant
that has actually read it. Stripe one-time purchases and memberships through
one idempotent webhook path with forward-only state machines; product review
and refunds as durable workflows that wait days for a human; RAG on pgvector
with structure-aware chunking and MMR re-ranking; a traced Claude agent gated
by plan and quota; a self-hosted edition unlocked by a signed license. Five
end-to-end flows tested on real Postgres in CI. English and Vietnamese.
`Next.js 15` `Prisma` `pgvector` `Stripe` `agent-runtime` `durable-workflow`

**[agent-runtime](https://github.com/tientran1234/agent-runtime)** — The part of
an LLM agent that is not the model: a bounded tool loop where no tool runs on
invalid input, after a refusal, or past a timeout; memory that trims in whole
turns so tool calls and results are never split; tracing with per-model cost;
a fallback chain keyed on the provider's retryable verdict; SSE. Anthropic
adapter on the official SDK, scripted fake for offline tests. 32 tests.
`TypeScript` `@anthropic-ai/sdk` `Zod`

**[durable-workflow](https://github.com/tientran1234/durable-workflow)** — Write
a multi-step process as one async function; run it across crashes and days of
waiting with every side effect happening exactly once. Replay-based execution
over an append-only history, memoised steps, retries as persisted wake times,
pause/resume on signals (early signals buffered), nondeterminism detection,
optimistic concurrency, and a Postgres store that leases work with
`FOR UPDATE SKIP LOCKED`. 22 tests, 5 against a real Postgres in CI.
`TypeScript` `PostgreSQL`

**[subscription-billing](https://github.com/tientran1234/subscription-billing)** —
Stripe subscriptions built to be correct where billing usually goes wrong:
signed webhooks read as raw bytes, an idempotent event log (the insert is the
lock), a forward-only state machine enforced by a conditional `UPDATE` in
Postgres, entitlements derived on read so a cancelled tenant loses access on
the next request, and hashed API keys with scopes and monthly quota. 40 tests,
12 against a real Postgres in CI. English and Vietnamese.
`Next.js 15` `Prisma` `PostgreSQL` `Stripe`

**[offline-license](https://github.com/tientran1234/offline-license)** — Software
licensing that works with the network unplugged. Ed25519-signed license tokens,
feature entitlements and limits, machine binding as an HMAC so the token
reveals nothing about the machine, and clock-rollback detection with an
in-memory high-water mark persisted through atomic writes. Zero dependencies,
37 tests.
`TypeScript` `node:crypto`

## Stack

| | |
|---|---|
| Backend | Node.js, NestJS, Express, Hono, REST, WebSocket, gRPC |
| Frontend | React, Next.js (App Router), TypeScript, Tailwind, TanStack Query |
| Data | PostgreSQL, Prisma, MySQL, MongoDB, DynamoDB, Redis, Qdrant |
| Cloud & CI | AWS (Lambda, DynamoDB, S3), GKE, Docker, Kubernetes, GitHub Actions, GitLab CI |
| Payments | Stripe, PayOS |
| AI | LLM integration (OpenAI, Anthropic, Ollama), agent tool-calling, RAG |

## Contact

tranngoctien29112003@gmail.com
