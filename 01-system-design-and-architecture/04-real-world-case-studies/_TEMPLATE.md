# Design [System Name]

> One-line framing: what this system does and who it's for.

## 1. Requirements

**Functional**
- ...

**Non-functional**
- Scale: (users, TPS, data volume — real numbers, even if approximate)
- Latency targets
- Consistency requirements (and *why* — what breaks if this is eventually
  consistent instead of strong?)
- Compliance/regulatory constraints, if any

**Out of scope** (be explicit — this is what separates a real design from
an interview answer that tries to cover everything)

## 2. Back-of-envelope estimation

- Traffic: reads/sec, writes/sec
- Storage: growth per day/month/year
- Bandwidth

## 3. High-level design

(Diagram — even ASCII/mermaid is fine to start)

Walk through the request path for the 1-2 most important flows end to end.

## 4. Data model

- Core entities and relationships
- Why relational/NoSQL/hybrid, and what you'd change if scale 10x'd

## 5. Deep dive: the hard part

Pick the 1-2 decisions that actually mattered — the thing that would fail
a system review if gotten wrong. (e.g., for a ledger: how do you guarantee
no double-spend under concurrent writes? For a matching engine: how do you
guarantee price-time priority under load?)

## 6. Failure modes & how it degrades

- What happens when [dependency] goes down?
- What's the blast radius of [component] failing?
- Graceful degradation vs hard failure — which parts get which, and why

## 7. Security & compliance notes

- AuthN/AuthZ approach
- Data classification (what's PII/PCI/financial data, how it's handled)
- Relevant compliance surface (note: architectural framing only, not legal
  advice — compliance requirements are jurisdiction-specific and change
  over time, so flag that readers should verify current requirements)

## 8. What we'd do differently

The section most system design content skips entirely. What did production
teach you that the initial design missed? This is the credibility section —
it's also usually the most-shared part of a post like this.

## 9. Trade-offs summary

| Decision | Option chosen | Alternative | Why |
|---|---|---|---|
| | | | |

---
*Have you built something similar and made a different trade-off? Open an
issue or PR — this repo is meant to be argued with, not just read.*
