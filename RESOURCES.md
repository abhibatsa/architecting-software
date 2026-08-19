# Resources

Curated, not comprehensive — books, papers, and blogs actually worth your
time, cross-linked from the topics they support rather than listed for
their own sake.

## 📚 Books

- **Designing Data-Intensive Applications** — Martin Kleppmann. The single
  most cited distributed-systems book for a reason; if you only read one
  book from this list, make it this one.

## 🗞️ Foundational distributed systems papers

Worth reading in full, not just skimming summaries — these are short and
the reasoning is more valuable than the conclusions:

- **The Google File System** (Ghemawat, Gobioff, Leung)
- **MapReduce: Simplified Data Processing on Large Clusters** (Dean, Ghemawat)
- **Dynamo: Amazon's Highly Available Key-value Store** (DeCandia et al.)
- **Bigtable: A Distributed Storage System for Structured Data** (Chang et al.)
- **Spanner: Google's Globally-Distributed Database** (Corbett et al.)
- **ZooKeeper: Wait-free coordination for Internet-scale systems** (Hunt et al.)
- **Paxos Made Simple** (Lamport) — more approachable starting point than
  the original Part-Time Parliament paper before attempting that one

## 📜 Engineering blog posts worth reading

Real production write-ups, not marketing:

- Stripe — how their payments API evolved over a decade
- Airbnb Engineering — how they avoid double payments in a distributed
  payments system (directly relevant to
  [idempotency](./01-system-design-and-architecture/01-core-concepts/idempotency-and-exactly-once-delivery.md))
- Discord Engineering — how they store trillions of messages
- Slack Engineering — real-time messaging architecture

## 🎥 Other channels worth following

For different angles than what's covered here — company-specific interview
walkthroughs, broader DSA + system design coverage:

- ByteByteGo
- System Design Interview (Study channel)

## How this list is maintained

Kept deliberately short. Anything added here should be something actually
read/watched and found genuinely useful — not a comprehensive index of
everything that exists on the topic. If it doesn't clear that bar, it
doesn't belong here.
