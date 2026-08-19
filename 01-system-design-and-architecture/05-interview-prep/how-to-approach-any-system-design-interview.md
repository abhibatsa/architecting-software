# How to approach any system design interview

A repeatable framework — the same one whether you're asked to design a URL
shortener or a payments platform. Interviewers aren't scoring whether you
land on "the right answer" (there usually isn't one) — they're scoring
whether you think like someone who could own this system in production.

This framework synthesizes the approach used across most credible system
design interview prep resources (structured breakdowns like HelloInterview's
delivery framework, ByteByteGo/AlgoMaster-style estimation-first approaches,
and *Designing Data-Intensive Applications* as the underlying theory) into
one sequence — cross-referenced in [`RESOURCES.md`](../../../RESOURCES.md)
if you want to go deeper on any single stage.

## The sequence (roughly 45 minutes)

### 1. Clarify requirements (5 min) — don't skip this under pressure
Ask before designing anything:
- **Functional**: what must the system do? Get 3-5 core use cases, not
  every edge case.
- **Non-functional**: scale (users, requests/sec), latency expectations,
  consistency requirements, read:write ratio.
- **Explicitly state what's out of scope.** "I'm going to assume we don't
  need to support X" is a strong signal — it shows you know the difference
  between core and peripheral.

**Common mistake:** jumping straight to a design because you recognize the
question. Interviewers notice — and it skips the part that's actually being
scored.

### 2. Back-of-envelope estimation (5 min)
Convert requirements into numbers: requests/sec (average and peak), storage
growth, bandwidth. See
[`scalability-and-back-of-envelope-estimation.md`](../01-core-concepts/scalability-and-back-of-envelope-estimation.md)
for the exact method. These numbers should drive every design decision
after this point — refer back to them out loud.

### 3. High-level design (10-15 min)
Draw the major components and how a request flows through them. Keep it
simple first — client, API layer, service, database. Resist the urge to
add caching/queues/CDN before you've justified why the simple version
doesn't work.

**Say the trade-off out loud** every time you add a component: "I'm adding
a cache here because [specific reason tied to your estimation numbers]."

### 4. Deep dive (15-20 min) — this is where the interview is actually won
The interviewer will steer you toward 1-2 components to go deeper on.
Common deep-dive territory:
- Data model — see [`data-modeling-relational-vs-nosql.md`](../01-core-concepts/data-modeling-relational-vs-nosql.md)
- Scaling a specific component — see [`sharding-and-partitioning.md`](../01-core-concepts/sharding-and-partitioning.md)
- Consistency guarantees — see [`consistency-models-strong-vs-eventual.md`](../01-core-concepts/consistency-models-strong-vs-eventual.md)
- Handling failure/retries — see [`idempotency-and-exactly-once-delivery.md`](../01-core-concepts/idempotency-and-exactly-once-delivery.md)

This is where "I've actually built this" separates from "I've read about
this." Bring a real constraint you've hit, not just the textbook answer.

### 5. Address bottlenecks & failure modes (5 min)
- What's the single point of failure in your design, and how does it fail?
- What happens under 10x the load you estimated?
- Where would you add monitoring/alerting to know this broke before a
  customer tells you?

### 6. Wrap-up (2 min)
Summarize the design in 3 sentences. State 1-2 things you'd do differently
with more time/information — this signals self-awareness, which is exactly
what "what we'd do differently" sections across this repo are modeling.

## The meta-skill interviewers are actually scoring

Not "did you draw the right boxes" — it's:
- **Did you drive the conversation**, or wait to be told what to do next?
- **Did you justify decisions with the numbers you estimated**, or with
  vague intuition ("this is more scalable")?
- **Did you know what you didn't know**, and say so, instead of bluffing?

## Related
- [`common-questions-index.md`](./common-questions-index.md) — practice
  prompts mapped to the relevant docs in this repo
- [`level-calibration-mid-vs-senior-vs-staff-vs-director.md`](./level-calibration-mid-vs-senior-vs-staff-vs-director.md) —
  how the bar shifts by level
