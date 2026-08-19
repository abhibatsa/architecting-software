# Trade-offs Index

Every "X vs Y" decision covered across this repo, in one scannable table.
Nothing here is duplicated content — each row links to wherever the full
write-up actually lives.

| Trade-off | Lives in | Status |
|---|---|---|
| Strong vs eventual consistency | [`01-core-concepts`](./01-core-concepts/consistency-models-strong-vs-eventual.md) | ✅ Published |
| Relational vs NoSQL | [`01-core-concepts`](./01-core-concepts/data-modeling-relational-vs-nosql.md) | ✅ Published |
| REST vs gRPC vs GraphQL | [`03-apis-and-microservices`](./03-apis-and-microservices) | 🔜 Not yet published |
| Vertical vs horizontal scaling | [`01-core-concepts`](./01-core-concepts) | 🔜 Not yet published |
| Range-based vs hash-based vs geo-based sharding | [`01-core-concepts`](./01-core-concepts/sharding-and-partitioning.md) | ✅ Published (covered within the sharding post) |
| Sync vs async replication | [`06-database-fundamentals`](./06-database-fundamentals) | 🔜 Not yet published |
| Read-through vs write-through caching | [`01-core-concepts`](./01-core-concepts) | 🔜 Not yet published |
| Batch vs stream processing | [`01-core-concepts`](./01-core-concepts) | 🔜 Not yet published |
| Stateful vs stateless design | [`07-architectural-patterns`](./07-architectural-patterns) | 🔜 Not yet published |
| Push vs pull architecture | [`07-architectural-patterns`](./07-architectural-patterns) | 🔜 Not yet published |
| REST vs RPC | [`03-apis-and-microservices`](./03-apis-and-microservices) | 🔜 Not yet published |
| Synchronous vs asynchronous communication | [`03-apis-and-microservices`](./03-apis-and-microservices) | 🔜 Not yet published |
| Concurrency vs parallelism | [`01-core-concepts`](./01-core-concepts) | 🔜 Not yet published |
| Latency vs throughput vs bandwidth | [`01-core-concepts`](./01-core-concepts) | 🔜 Not yet published |
| ISV-on-rails vs licensed PA (payments-specific) | [`02-fintech-wealthtech-insuretech-case-studies`](./02-fintech-wealthtech-insuretech-case-studies) | 🔜 Not yet published |

## Why this file exists instead of a separate folder

Every trade-off above already belongs to a specific topic doc — duplicating
that content into a standalone `08-tradeoffs` folder would mean maintaining
the same explanation in two places. This index exists purely as a second
way to *navigate* content that already lives elsewhere: useful for someone
who thinks "I need to understand X vs Y" before they think "I need to learn
about caching."

## Contributing a trade-off

If you're writing a new topic doc and it centers on a genuine trade-off,
add a row here linking back to it — don't write the comparison twice.
