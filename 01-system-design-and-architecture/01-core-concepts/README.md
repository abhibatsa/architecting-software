# Core Concepts

Production-grounded explainers on the building blocks of system design —
each one follows the same format: what it is, when it matters in
production, a real example, common mistakes, a trade-offs table, and a
**Best Practices** section (or, where a real production story exists,
**What we'd do differently**).

Each topic also has a matching short video — see the 🎥 column below.

## 📚 Topics

| Topic | Doc | Video |
|---|---|---|
| Idempotency & exactly-once delivery | [Read →](./idempotency-and-exactly-once-delivery.md) | 🎥 Coming soon |
| Scalability & back-of-envelope estimation | [Read →](./scalability-and-back-of-envelope-estimation.md) | 🎥 Coming soon |
| Consistency models: strong vs eventual | [Read →](./consistency-models-strong-vs-eventual.md) | 🎥 Coming soon |
| Data modeling: relational vs NoSQL | [Read →](./data-modeling-relational-vs-nosql.md) | 🎥 Coming soon |
| Sharding & partitioning | [Read →](./sharding-and-partitioning.md) | 🎥 Coming soon |
| Caching patterns & invalidation | [Read →](./caching-patterns-and-invalidation.md) | 🎥 Coming soon |
| Messaging: queues vs streams | [Read →](./messaging-queues-vs-streams.md) | 🎥 Coming soon |
| Outbox pattern & transactional messaging | [Read →](./outbox-pattern-and-transactional-messaging.md) | 🎥 Coming soon |
| CAP & PACELC in practice | [Read →](./cap-and-pacelc-in-practice.md) | 🎥 Coming soon |
| Rate limiting & backpressure | [Read →](./rate-limiting-and-backpressure.md) | 🎥 Coming soon |
| Distributed locking & coordination | [Read →](./distributed-locking-and-coordination.md) | 🎥 Coming soon |
| Load balancing strategies | [Read →](./load-balancing-strategies.md) | 🎥 Coming soon |
| Database replication & failover | [Read →](./database-replication-and-failover.md) | 🎥 Coming soon |

## Format every doc follows

1. **What it is** (2-3 sentences, no fluff)
2. **When it matters in production** (the part textbooks skip)
3. **A real example** from something actually built
4. **Common mistakes** seen or made
5. **Trade-offs table** (option vs. when to use it)
6. **Best Practices** — genuinely useful, defensible guidance for the
   topic. Where a real production incident exists to draw on instead,
   that section becomes **What we'd do differently** — a real story, not
   a placeholder. Don't fake the latter; "Best Practices" is the honest
   default for evergreen concept docs.

All 13 topics above are now published, complete with diagrams.
