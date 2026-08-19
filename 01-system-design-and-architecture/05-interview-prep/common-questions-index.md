# Common system design interview questions — indexed, not re-answered

Every common prompt maps to the relevant doc(s) already in this repo. The
point of this file is to save you from re-deriving fundamentals mid-answer
— study the linked doc, then practice assembling it into a full design
using the [framework](./how-to-approach-any-system-design-interview.md).

## How to use this index

For each prompt: read the linked core-concept/case-study docs *before*
attempting a mock answer, then do a timed 45-minute practice run using the
framework. The docs give you the building blocks; assembling them under
time pressure is the actual skill being tested.

## Foundational / infrastructure

| Prompt | Study these docs |
|---|---|
| Design a URL shortener | [`data-modeling-relational-vs-nosql.md`](../01-core-concepts/data-modeling-relational-vs-nosql.md), [`scalability-and-back-of-envelope-estimation.md`](../01-core-concepts/scalability-and-back-of-envelope-estimation.md) |
| Design a rate limiter | [`idempotency-and-exactly-once-delivery.md`](../01-core-concepts/idempotency-and-exactly-once-delivery.md) *(same "enforce at the server" principle)* — dedicated rate-limiting doc 🔜 not yet published |
| Design a distributed cache | 🔜 caching doc not yet published — see [`consistency-models-strong-vs-eventual.md`](../01-core-concepts/consistency-models-strong-vs-eventual.md) for the invalidation trade-off underneath it |
| Design a distributed key-value store | [`sharding-and-partitioning.md`](../01-core-concepts/sharding-and-partitioning.md), [`consistency-models-strong-vs-eventual.md`](../01-core-concepts/consistency-models-strong-vs-eventual.md) |
| Design a load balancer | 🔜 not yet published |
| Design a CDN | 🔜 not yet published |
| Design an authentication system | 🔜 not yet published |

## Consumer-scale products

| Prompt | Study these docs |
|---|---|
| Design WhatsApp / a messaging system | [`consistency-models-strong-vs-eventual.md`](../01-core-concepts/consistency-models-strong-vs-eventual.md) *(delivery guarantees)*, [`sharding-and-partitioning.md`](../01-core-concepts/sharding-and-partitioning.md) |
| Design Instagram / a social feed | [`data-modeling-relational-vs-nosql.md`](../01-core-concepts/data-modeling-relational-vs-nosql.md) *(fan-out on write vs read)* |
| Design a notification service | [`idempotency-and-exactly-once-delivery.md`](../01-core-concepts/idempotency-and-exactly-once-delivery.md) *(duplicate sends are the same bug class as duplicate charges)* |
| Design YouTube / Netflix | See [`04-real-world-case-studies`](../04-real-world-case-studies) — closest existing case study once published |
| Design an e-commerce platform (Amazon-style) | [`02-fintech-wealthtech-insuretech-case-studies`](../02-fintech-wealthtech-insuretech-case-studies) *(inventory + payment overlap directly)* |

## Payments & fintech (this repo's actual differentiator — go deep here)

| Prompt | Study these docs |
|---|---|
| Design a payment system | [`idempotency-and-exactly-once-delivery.md`](../01-core-concepts/idempotency-and-exactly-once-delivery.md), [`02-fintech-wealthtech-insuretech-case-studies`](../02-fintech-wealthtech-insuretech-case-studies) |
| Design UPI / a real-time payment rail | [`02-fintech-wealthtech-insuretech-case-studies`](../02-fintech-wealthtech-insuretech-case-studies) — closest to direct build experience in this repo |
| Design a digital wallet | Same as above, plus [`consistency-models-strong-vs-eventual.md`](../01-core-concepts/consistency-models-strong-vs-eventual.md) for the balance-consistency requirement |
| Design a fraud detection pipeline | [`02-fintech-wealthtech-insuretech-case-studies`](../02-fintech-wealthtech-insuretech-case-studies) |

## Distributed systems / infrastructure-heavy

| Prompt | Study these docs |
|---|---|
| Design a distributed message queue (Kafka-style) | 🔜 messaging doc not yet published |
| Design a distributed job scheduler | 🔜 not yet published |
| Design a distributed locking service | 🔜 `distributed-locking-and-coordination.md` not yet published |
| Design a web crawler | 🔜 not yet published |

## A note on this list vs "answer 30 companies' questions"

This index is deliberately not exhaustive the way some prep sites are —
the strategy for this repo is depth on payments/fintech-adjacent systems
(where real build experience exists) over shallow coverage of every
consumer app. If a prompt isn't listed here, the framework doc plus the
closest analogous case study above should still get you most of the way.

## Related
- [`how-to-approach-any-system-design-interview.md`](./how-to-approach-any-system-design-interview.md)
- [`../TRADEOFFS-INDEX.md`](../TRADEOFFS-INDEX.md) — if a question hinges on
  a specific "X vs Y" call, check here first
