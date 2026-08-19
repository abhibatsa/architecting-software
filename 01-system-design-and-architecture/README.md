# System Design & Architecture — From Requirement to Production

Most system design content teaches you to survive an interview whiteboard.
This teaches you to survive production — the same design, but with the
security review, the on-call rotation, and the cost review still ahead of it.

## Why this is different

- **Grounded in real builds**, not hypotheticals — payment platforms
  (ledger design, cross-border rails), broker-scale trading infra, neo-banking
  for underserved markets, and AI/SaaS products actually shipped.
- **Requirement → Production**, not "design a system in 45 minutes." Every
  case study covers: requirements & constraints → high-level design →
  data model → API design → scaling → security → failure modes → what we'd
  do differently.
- **Fintech/Wealthtech/Insuretech-heavy**, because that's where the design
  constraints are hardest (money can't be eventually-consistent when it
  shouldn't be, compliance isn't optional, fraud is adversarial).

## 📂 Structure

### [01 — Core Concepts](./01-core-concepts)
The building blocks, explained with production trade-offs, not just definitions.
- Scalability & load — vertical/horizontal, back-of-envelope estimation
- Consistency models — strong vs eventual, and *when it actually matters*
- Data modeling — relational vs NoSQL, sharding, partitioning strategies
- Caching — patterns, invalidation, cache stampede
- Messaging & event-driven design — queues, streams, outbox pattern
- CAP / PACELC in practice, not just theory
- Idempotency & exactly-once delivery (the thing most designs get wrong)
- Rate limiting & backpressure
- Distributed locking & coordination

### [02 — Fintech, Wealthtech & Insuretech Case Studies](./02-fintech-wealthtech-insuretech-case-studies)
The differentiated core of this repo.
- Double-entry ledger design (with reconciliation)
- Payment gateway / TSP architecture — auth, capture, settlement, refunds
- UPI-style real-time payment rails
- Cross-border payments & FIRA/compliance-aware design
- Fraud detection pipeline architecture
- Trading/brokerage order management system design
- Wealthtech portfolio & robo-advisory system design
- Insuretech claims processing & underwriting pipeline design
- KYC/AML pipeline architecture

### [03 — APIs & Microservices](./03-apis-and-microservices)
- REST vs gRPC vs GraphQL — when each actually wins
- API versioning strategies that don't break clients
- Microservices decomposition — bounded contexts, DDD in practice
- Service-to-service auth (mTLS, JWT, API keys) — trade-offs
- Saga pattern & distributed transactions
- API gateway design & BFF pattern
- Contract testing & backward compatibility

### [04 — Real-World Case Studies](./04-real-world-case-studies)
Full end-to-end designs, requirement-to-production:
- Design a payment platform (like Razorpay/Stripe) — ISV vs licensed PA trade-offs
- Design a UPI simulator / real-time settlement system
- Design a broker platform (order book, matching, settlement)
- Design a fraud/impersonation detection platform
- Design an AI test-generation SaaS (multi-tenant, usage-metered)
- Design a flex-workspace/marketplace platform

### [05 — Interview Prep](./05-interview-prep)
- Framework for approaching any system design interview (requirements →
  estimation → high-level design → deep dive → trade-offs)
- Level-calibrated expectations (mid vs senior vs staff vs director)
- Common company-style questions, answered with the same requirement→production
  rigor as the case studies above (not shortcuts)
- Leadership/behavioral stories mapped to architecture decisions (useful for
  Director/EM-level interviews where "why" matters as much as "what")

### [06 — Database Fundamentals](./06-database-fundamentals)
- ACID transactions, indexing, database types, scaling, replication, bloom
  filters, active-active vs active-passive architectures
- (SQL vs NoSQL and sharding live in `01-core-concepts` — cross-linked, not
  duplicated)

### [07 — Architectural Patterns](./07-architectural-patterns)
- Client-server, event-driven, serverless, peer-to-peer
- (Microservices architecture lives in `03-apis-and-microservices` —
  cross-linked, not duplicated)

## 🧭 How to use this repo

- New to system design → start at `01-core-concepts`
- Prepping for an interview → `05-interview-prep`, then cross-reference the
  relevant `04-real-world-case-studies`
- Building in fintech/wealthtech/insuretech → `02` is your home base
- Want the "why", not just the "what" → every case study includes a
  **trade-offs & what we'd do differently** section — that's the part most
  repos skip
- Looking for a specific "X vs Y" decision → check
  [`TRADEOFFS-INDEX.md`](./TRADEOFFS-INDEX.md) first, it cross-links every
  comparison in the repo in one table

## ✍️ Content status

| Section | Status |
|---|---|
| Core Concepts | 🟡 In progress (5 of 13 published) |
| Fintech/Wealthtech/Insuretech Case Studies | 🟡 In progress |
| APIs & Microservices | ⚪ Not started |
| Real-World Case Studies | ⚪ Not started |
| Interview Prep | ⚪ Not started |
| Database Fundamentals | ⚪ Not started |
| Architectural Patterns | ⚪ Not started |

-------- *** --------
