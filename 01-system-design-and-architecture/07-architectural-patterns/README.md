# Architectural Patterns

The big-picture shapes a system can take, before you get into the
component-level decisions. Same format as the rest — what it is, when it
matters in production, a real example, common mistakes, trade-offs table.

## 📚 Topics

| Topic | Doc |
|---|---|
| Client-server architecture — the default, and when it stops being enough | 🔜 Not yet published |
| Event-driven architecture — decoupling via events, and its debugging cost | 🔜 Not yet published |
| Serverless architecture — where it genuinely wins vs where it just hides ops cost | 🔜 Not yet published |
| Peer-to-peer architecture — rare in product systems, but worth knowing why | 🔜 Not yet published |

*(Microservices architecture is covered in depth in
[`03-apis-and-microservices`](../03-apis-and-microservices) — cross-linked
from here rather than duplicated.)*

## How this differs from Core Concepts

Core Concepts covers building blocks (caching, sharding, consistency).
This folder covers the **overall shape** a system takes — the pattern you'd
name in the first five minutes of a design interview, before you get into
any of those building blocks.

## Suggested starting point

`Event-driven architecture` — directly reusable in the fintech case
studies (reconciliation, fraud detection) where event-driven design is the
actual production pattern, not a theoretical choice.
