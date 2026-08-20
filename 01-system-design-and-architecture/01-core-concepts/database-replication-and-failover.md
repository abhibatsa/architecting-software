# Database replication & failover

**Read time:** 3 min

---

A single database instance is a single point of failure by definition.
Replication exists to fix that — and failover is what actually happens
the moment it's tested for real, usually at the worst time.

## Replication topologies

- **Single-leader (primary-replica):** one node accepts writes, replicates
  to one or more read replicas. Simple mental model, the most common
  setup — but the leader is still a single write bottleneck and a single
  point of failure until failover happens.
- **Multi-leader:** more than one node accepts writes, replicating to each
  other. Solves the single-write-bottleneck problem, but introduces
  **write conflicts** — two leaders can accept conflicting writes to the
  same record before they've synced, and something has to resolve that
  (last-write-wins, custom merge logic, or application-level conflict
  resolution).
- **Leaderless:** any node can accept reads and writes (Dynamo-style,
  used by Cassandra). Highly available, but requires quorum-based
  read/write logic to maintain any consistency guarantee at all.

## Sync vs async replication

**Synchronous:** the leader waits for the replica(s) to confirm the write
before acknowledging it to the client. Zero data loss on failover, but
adds latency to every write, and if a replica is slow, the leader's writes
slow down with it.

**Asynchronous:** the leader acknowledges the write immediately, replicates
in the background. Fast writes, but a real risk: if the leader fails
before a write has replicated, that write is lost on failover.

Most production systems land on a middle ground — **semi-synchronous**:
wait for at least one replica to confirm (not all), balancing latency
against durability.

## Failover: where the real complexity lives

When the leader dies, something has to happen automatically, or you're
paging a human at 3am to manually promote a replica. Automated failover
introduces its own hard problems:

- **Detecting a real failure vs a network blip.** Promote too eagerly on
  a transient network partition, and you can end up with two nodes both
  believing they're the leader — a **split-brain** scenario, where writes
  start landing on both, diverging state that's painful to reconcile
  later.
- **Replication lag at failover time.** If the promoted replica was behind
  the old leader when it died, any writes acknowledged by the old leader
  but not yet replicated are gone — this is the async-replication data
  loss risk actually materializing.
- **Failback.** Once the old leader recovers, is it safely reintroduced as
  a replica, or does its data need reconciliation first? A naive failback
  can reintroduce stale or conflicting data.

## The actual skill

Replication topology is a data-loss-tolerance decision, not just a
performance one. A system where losing the last few seconds of writes on
a rare failover is genuinely fine (e.g. non-critical logging) can use
async replication for speed. A ledger or payment system usually can't
accept that risk, and needs to pay the sync/semi-sync latency cost
instead — same underlying trade-off as
[`consistency-models-strong-vs-eventual.md`](./consistency-models-strong-vs-eventual.md),
applied specifically to the replication layer.

## What we'd do differently

*ToDo*

---

**Has an automated failover ever made things worse for you — split-brain,
lost writes, or a bad failback?**

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
