# Leadership stories mapped to architecture decisions

For director/EM-level interviews, the design isn't the whole answer — "why
did you make this call, and how did you lead the team through it" carries
equal or more weight. This doc gives the template and two fully worked
examples, built from the same real experiences already documented in this
repo's case studies.

## Why this format, specifically

A pure STAR story ("Situation, Task, Action, Result") answers the
leadership question but loses the technical credibility. A pure
architecture walkthrough proves technical depth but skips the leadership
signal entirely. This template forces both into one story, because that's
literally what the interview is scoring at this level.

## The template

```markdown
### [Decision name]

**The architecture decision:** What was actually decided, in one sentence.

**Why it mattered beyond the code:** What would have gone wrong for the
business/customers if this wasn't made correctly — not the technical
failure mode, the business one.

**How I drove the decision:** Did you make the call unilaterally, build
consensus, escalate, or delegate the decision to someone closer to the
problem? Be honest about which — interviewers can tell when this is
embellished.

**Leading the team through it:** What was hard about getting this shipped
that had nothing to do with the technology — pushback, timeline pressure,
a team member who disagreed, a dependency on another team?

**What we'd do differently:** Same non-negotiable section as every case
study in this repo. At this level, this is often the most-remembered part
of the answer.
```

## Worked example 1 — idempotency in a payments flow

*(Architecture reference: [`idempotency-and-exactly-once-delivery.md`](../01-core-concepts/idempotency-and-exactly-once-delivery.md))*

**The architecture decision:** Added a transaction-scoped idempotency key
to the payment gateway integration, enforced server-side, after customers
were charged twice on retried requests.

**Why it mattered beyond the code:** This wasn't a UX bug — it was a
trust and compliance issue. Every double-charge became a support ticket,
a refund process, and a data point in whether customers trusted the
platform with their money during an early, trust-critical launch phase.

**How I drove the decision:** Once the pattern was confirmed from support
tickets, I made the call to treat this as a stop-ship-severity fix rather
than a backlog item, and pulled engineers off planned feature work for the
sprint. That trade-off — feature velocity vs a trust-critical correctness
bug — was mine to own, and I communicated it upward as a deliberate
prioritization call, not an emergency reaction.

**Leading the team through it:** The harder leadership problem wasn't the
fix itself — it was that the team's first instinct was a client-side
retry-guard, which doesn't actually solve the problem (the client can't
guarantee delivery). I had to walk the team through *why* the fix needed
to live server-side, which meant slowing down to align on the mental model
before anyone touched code — otherwise we'd have shipped a fix that felt
done but wasn't.

**What we'd do differently:** This should have been a launch-blocking
requirement, not a post-incident fix — idempotency at the payment layer is
not something you retrofit gracefully. I'd add it to the non-negotiable
checklist for any future payment-adjacent integration, not rely on an
incident to surface it.

---

## Worked example 2 — [reconciliation engine / your next story]

*(Architecture reference: link to the relevant case study once published)*

**The architecture decision:** *(fill in)*

**Why it mattered beyond the code:** *(fill in)*

**How I drove the decision:** *(fill in)*

**Leading the team through it:** *(fill in)*

**What we'd do differently:** *(fill in)*

---

## Building your own set

Aim for 4-6 stories total, each mapped to a different *kind* of leadership
moment — don't repeat the same shape:

- A correctness/trust bug you had to reprioritize around (example 1 above)
- A build-vs-buy or migration call with real organizational cost
- A time you were wrong and had to reverse a decision publicly
- A disagreement with a peer or your own manager that you had to resolve
- A decision made under genuine ambiguity, before the data was clear

## Related
- [`level-calibration-mid-vs-senior-vs-staff-vs-director.md`](./level-calibration-mid-vs-senior-vs-staff-vs-director.md) —
  why this section carries more weight at director level specifically
