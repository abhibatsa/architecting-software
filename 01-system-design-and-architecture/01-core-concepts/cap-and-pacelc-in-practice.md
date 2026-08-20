# CAP & PACELC in practice

**Read time:** 3 min

---

CAP theorem gets quoted constantly and understood shallowly. "Pick two of
three" is the line everyone remembers — and it's the part that's actually
a little misleading.

## What CAP actually says

**C**onsistency, **A**vailability, **P**artition tolerance — and the real
claim isn't "pick any two of three." It's: **when a network partition
happens, you must choose between consistency and availability. Partition
tolerance isn't optional** — in any real distributed system, network
partitions *will* happen, so you don't get to "not pick" P. The actual
choice CAP forces is CP vs AP, only during a partition.

- **CP (consistency over availability):** during a partition, the system
  refuses requests it can't guarantee are consistent, rather than risk
  returning stale/conflicting data. Example: a system that returns an
  error rather than risk two nodes disagreeing on an account balance.
- **AP (availability over consistency):** during a partition, the system
  keeps serving requests from whatever node is reachable, accepting that
  different nodes might temporarily disagree. Example: a shopping cart
  that stays usable even if it briefly shows slightly stale contents.

## Why PACELC is the more useful framework

CAP only describes behavior **during a partition** — but partitions are
rare. Most of the time, the system is running normally, and there's still
a real trade-off happening: consistency vs latency. PACELC captures both:

> **If Partition, choose Availability or Consistency; Else (normal
> operation), choose Latency or Consistency.**

This is the more honest framing, because it forces you to also answer:
even when everything's healthy, are you willing to wait for a
consistency-guaranteeing round-trip (like a quorum write), or do you want
the lowest possible latency and accept some staleness?

## Mapping real systems

| System | Partition behavior | Normal-operation behavior |
|---|---|---|
| Traditional single-region relational DB (strong consistency) | CP-leaning | Consistency over latency (PC) |
| DynamoDB, Cassandra (tunable) | AP by default, tunable toward CP per-query | Latency over consistency by default (PA/EL) |
| Spanner | CP, using synchronized clocks (TrueTime) to minimize the latency cost of consistency | Still pays a real latency cost for global consistency (PC/EC) |

## The actual skill

Same lesson as strong-vs-eventual consistency (see
[`consistency-models-strong-vs-eventual.md`](./consistency-models-strong-vs-eventual.md)) —
this isn't a whole-system decision, it's per data type. A payments ledger
justifies paying the latency cost for consistency. A "users currently
online" counter doesn't. Most production systems are a deliberate mix,
not a single CAP classification stamped on the whole architecture.

## What we'd do differently

*ToDO*

---

**Where in your stack are you actually CP, and where are you actually AP —
and was that a deliberate choice, or an accident of which database someone
picked two years ago?**

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
