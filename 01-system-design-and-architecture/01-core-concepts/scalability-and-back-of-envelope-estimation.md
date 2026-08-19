# Scalability & back-of-envelope estimation

**Watch (~1.5 min):** [YouTube link] · **Read time:** 3 min

---

You don't need Google's traffic to hit Google's problems.

Most teams either massively over-engineer for scale they'll never see, or
get blindsided because nobody did the napkin math before shipping. Both
mistakes come from the same root cause: skipping estimation and jumping
straight to architecture.

## Why rough math beats no math

Back-of-envelope estimation isn't about precision — it's about being
roughly right, fast, so your architecture decisions match your actual scale
instead of your imagined scale.

Four numbers get you 80% of the way there:

- **Requests per second** (average and peak)
- **Storage growth per day**
- **Read-to-write ratio**
- **Peak-to-average traffic multiplier**

Ten minutes of this math saves weeks of premature — or way-too-late —
architecture decisions.

## A worked example

System with 1 million daily active users, each making 10 requests a day.

```
10,000,000 requests/day
÷ 86,400 seconds/day
≈ 115 requests/second (average)
```

Average traffic isn't what breaks you — peak does. A typical peak-to-average
ratio is 3-5x for consumer apps (higher for anything with predictable spikes
— flash sales, market open, payday):

```
115 avg RPS × 4 (peak multiplier)
≈ 460 requests/second at peak
```

That single multiplier is the difference between a system that falls over
during your busiest hour and one that doesn't. If you designed for 115 RPS
because that's what the average said, you built a system that fails exactly
when it matters most.

## Storage, quickly

If each request writes ~1KB of data and 30% of requests are writes:

```
10M requests/day × 30% writes × 1KB
= 3GB/day
≈ 1.1TB/year
```

Enough to tell you whether you need a sharding conversation in month 3 or
year 3 — a very different set of decisions.

## The actual skill

It's not memorizing formulas — it's knowing which four numbers matter for
*this* system, and being willing to state an estimate with a `~` in front of
it instead of waiting for perfect data that never comes. An architecture
review with rough-but-directionally-right numbers beats one with none at
all, every time.

## What we'd do differently

*(Fill this in with a real story once you've shipped this in production —
this section is what separates the post from a textbook definition.)*

---

**What's the last estimate you got wrong** — did you over-build or
under-build? Open an issue or drop a comment on the video.

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
