# Level calibration: mid vs senior vs staff vs director

Same question, same 45 minutes — completely different bar. This is the
single most common reason strong engineers get miscalibrated feedback: they
answer the question well, just not at the altitude the level requires.

*Titles vary by company (L4/L5/L6/L7, IC vs manager tracks, etc.) — treat
the categories below as a rough mapping, and verify against the specific
company's leveling guide when you have one.*

## Mid-level (SDE II / L4-ish)

**What's actually being scored:** can you design a working system for a
well-scoped problem, using the fundamentals correctly?

- Expected to land on a *correct*, functioning design without heavy
  interviewer steering
- Deep dives are usually interviewer-selected, not self-initiated
- Trade-off discussion can be somewhat textbook — "SQL because we need
  ACID" is an acceptable level of depth
- **Common gap that costs points:** skipping requirements clarification,
  or not doing back-of-envelope math before designing

## Senior (SDE III / L5-ish)

**What's actually being scored:** can you make the trade-offs *yourself*,
and justify them with the specific numbers of *this* system, not general
principles?

- Expected to proactively identify where the design needs to go deeper,
  without being asked
- Trade-off answers need to be situational: not "SQL because ACID" but
  "SQL here because our write pattern needs multi-row transactions across
  the ledger and inventory tables — a NoSQL model would need
  application-level compensation logic for the same guarantee"
- Expected to catch your own mistakes when probed, not need them pointed
  out
- **Common gap that costs points:** correct design, but every decision
  justified generically instead of tied to the specific requirements
  discussed 10 minutes earlier

## Staff (L6-ish)

**What's actually being scored:** can you reason about a system that's
bigger than what fits in one whiteboard — org boundaries, migration paths,
build-vs-buy, and the cost of being wrong?

- Expected to discuss how this system fits into a broader architecture —
  what other services depend on it, what happens during a migration from
  an existing system
- Expected to weigh **organizational** cost, not just technical cost — "this
  approach needs a dedicated on-call rotation" is a real trade-off at this
  level
- Should be comfortable saying "I'd prototype both and measure" instead of
  claiming certainty from a whiteboard
- **Common gap that costs points:** staying at senior-level technical depth
  without zooming out to system-of-systems and organizational trade-offs

## Director / EM (people-leadership track)

**What's actually being scored:** less "can you personally design this,"
more "can you set direction, make the call under ambiguity, and lead a
team through building it — including the parts that went wrong."

- The architecture still needs to be sound, but the interview weight shifts
  toward **why you made a call, how you got buy-in, and how you led through
  the fallout when it didn't go to plan**
- Expected to speak to trade-offs at the level of team structure, timeline,
  and stakeholder alignment, not just technical correctness
- "What we'd do differently" carries more weight than the original design —
  this is exactly the section this repo treats as non-negotiable in every
  case study, for the same reason
- See [`leadership-stories-mapped-to-architecture-decisions.md`](./leadership-stories-mapped-to-architecture-decisions.md)
  for how to prepare this specifically

## One test to self-calibrate

After answering a mock question, ask: **"Would my answer change if the
scale requirement 10x'd, or if I had to hand this off to a team I don't
manage?"** If the honest answer is "not really," you're probably answering
at a level below the one you're targeting.

## Related
- [`how-to-approach-any-system-design-interview.md`](./how-to-approach-any-system-design-interview.md) —
  the base framework this calibration sits on top of
