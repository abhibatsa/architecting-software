# Core Concepts

Each concept below should be its own `.md` file (or folder if it needs
diagrams). Suggested format for each:

1. **What it is** (2-3 sentences, no fluff)
2. **When it matters in production** (the part textbooks skip)
3. **A real example** from something you've actually built
4. **Common mistakes** you've seen or made
5. **Trade-offs table** (option vs. when to use it)

## Checklist

- [ ] `scalability-and-back-of-envelope-estimation.md`
- [ ] `consistency-models-strong-vs-eventual.md`
- [ ] `data-modeling-relational-vs-nosql.md`
- [ ] `sharding-and-partitioning.md`
- [ ] `caching-patterns-and-invalidation.md`
- [ ] `messaging-queues-vs-streams.md`
- [ ] `outbox-pattern-and-transactional-messaging.md`
- [ ] `cap-and-pacelc-in-practice.md`
- [ ] `idempotency-and-exactly-once-delivery.md`
- [ ] `rate-limiting-and-backpressure.md`
- [ ] `distributed-locking-and-coordination.md`
- [ ] `load-balancing-strategies.md`
- [ ] `database-replication-and-failover.md`

Start with `idempotency-and-exactly-once-delivery.md` or
`cap-and-pacelc-in-practice.md` — these are the two concepts candidates and
engineers get most confidently wrong, and they're exactly the kind of "I
learned this the hard way in production" content that differentiates this
repo from generic write-ups.
