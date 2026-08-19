# Database Fundamentals

The stuff that separates "I can draw a database icon on a diagram" from
"I've actually run one in production." Same format as Core Concepts — what
it is, when it matters in production, a real example, common mistakes,
trade-offs table.

## 📚 Topics

| Topic | Doc |
|---|---|
| ACID transactions — what each guarantee actually protects against | 🔜 Not yet published |
| Database indexing — B-trees, when an index helps vs hurts writes | 🔜 Not yet published |
| Database types — relational, document, key-value, columnar, graph, time-series | 🔜 Not yet published |
| Database scaling — read replicas → sharding → the order that actually works | 🔜 Not yet published |
| Data replication — sync vs async, and what you trade for each | 🔜 Not yet published |
| Bloom filters — what they're for and where they show up in real systems | 🔜 Not yet published |
| Database architectures — active-active vs active-passive | 🔜 Not yet published |

*(SQL vs NoSQL, sharding & partitioning already live in
[`01-core-concepts`](../01-core-concepts) — cross-linked from here rather
than duplicated.)*

## Why this folder exists

This was a real gap — the earlier Wave 1 scope covered data modeling and
sharding but skipped the fundamentals underneath them (ACID, indexing,
database types). For a repo built on "requirement to production," this is
non-negotiable ground: indexing trade-offs and ACID guarantees are exactly
where interviews probe deepest and where production incidents actually
happen.

## Suggested starting point

`ACID transactions` — pairs directly with the ledger/reconciliation
case studies in `02-fintech-wealthtech-insuretech-case-studies`, so the
production example practically writes itself.
