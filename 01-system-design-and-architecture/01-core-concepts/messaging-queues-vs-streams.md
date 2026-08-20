# Messaging: queues vs streams

**Read time:** 3 min

---

"Just put it on a queue" is one of the most overused pieces of system
design advice — and it glosses over a real decision: a message queue and
an event stream solve different problems, and picking the wrong one shows
up as pain months later, not immediately.

## Queues (RabbitMQ, SQS, ActiveMQ)

A message is delivered to **one consumer**, then it's gone — consumed and
typically removed from the queue. Built for **task distribution**: a job
needs to happen exactly once, by exactly one worker. Once consumed, the
message doesn't exist for anyone else to read.

Good fit: background job processing, sending an email, resizing an image,
processing a payment — work items that need to happen once, reliably, and
whose history nobody needs to replay later.

## Streams (Kafka, Kinesis, Pulsar)

A message (event) is written to a durable, ordered log and **retained**
for a configurable period. Multiple independent consumers can read the
same stream, each tracking their own position — one consumer doesn't
consume the message away from another.

Good fit: anything multiple systems need to react to independently (an
order-placed event that triggers inventory updates, fraud checks, and
analytics simultaneously), or anything where replay matters (rebuilding a
read model, reprocessing after a bug fix).

## The decision that actually matters

Ask: **does more than one system need to independently react to this
event, or does exactly one worker need to process this task?**

- One worker, one outcome, no replay needed → queue
- Multiple independent consumers, or replay/audit matters → stream

The mistake that costs teams the most: reaching for Kafka by default
because it's the trendier choice, then building elaborate consumer-group
management for what was actually a simple one-worker task queue the whole
time — or the reverse, building a task queue and then needing multiple
services to react to the same event, and bolting on fan-out logic that a
stream would have given for free.

## A production detail both share: at-least-once delivery

Neither queues nor streams typically guarantee exactly-once delivery
without extra work — most default to at-least-once. This means consumers
must be **idempotent** (see
[`idempotency-and-exactly-once-delivery.md`](./idempotency-and-exactly-once-delivery.md)) —
processing the same message twice should be safe, because it will
eventually happen.

## What we'd do differently

*(Fill this in with a real story once you've shipped this in production —
this section is what separates the post from a textbook definition.)*

---

**Queue or stream — which one did you pick wrong once, and what did it
cost you to fix?**

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
