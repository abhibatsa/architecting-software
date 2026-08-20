# Load balancing strategies

**Read time:** 3 min

---

"Put a load balancer in front of it" is step one in nearly every system
design answer. The actual algorithm behind that box matters more than
most diagrams let on.

## Common algorithms

- **Round robin:** requests distributed sequentially across servers, in
  order. Simple, but assumes every server and every request is roughly
  equal cost — a bad assumption the moment request costs vary widely.
- **Least connections:** routes to whichever server currently has the
  fewest active connections. Better than round robin when request
  durations vary significantly — a server stuck on a few slow requests
  won't keep getting piled onto.
- **Weighted round robin / weighted least connections:** same as above,
  but servers get a weight reflecting their actual capacity — useful
  during a rolling deploy when new and old instance types temporarily
  coexist with different specs.
- **IP hash / consistent hashing:** routes based on a hash of the client
  IP (or another key), so the same client consistently lands on the same
  server — needed for **session affinity** (sticky sessions), and the
  same underlying technique used in
  [`sharding-and-partitioning.md`](./sharding-and-partitioning.md) for a
  different purpose.
- **Least response time:** factors in both active connections and recent
  response times — most adaptive, most operationally complex.

## Layer 4 vs Layer 7

**Layer 4 (transport layer):** balances based on IP/port, doesn't inspect
request content — faster, lower overhead, but can't make routing decisions
based on what's actually in the request (URL path, headers, cookies).

**Layer 7 (application layer):** inspects the actual HTTP request — can
route `/api/*` to one service and `/static/*` to another, route based on a
header, or terminate TLS before forwarding. More overhead per request, but
necessary for anything beyond simple traffic splitting.

## Health checks: the part that actually prevents outages

A load balancer is only as good as its ability to detect an unhealthy
backend and stop routing to it. Two failure modes to design against:

- **False negatives (marking a healthy server unhealthy):** too aggressive
  a health check (e.g. failing on a single slow response) can pull healthy
  capacity out of rotation right when you need it most — under load.
- **False positives (routing to an actually-unhealthy server):** too
  lenient a check misses real failures, and requests keep getting sent to
  a server that can't serve them.

A shallow health check (is the process responding at all) is not the same
as a deep health check (can this instance actually reach its database
and dependencies) — a server can respond to a ping while being
functionally broken for real traffic.

## The mistake that actually hurts

Sticky sessions (IP hash) combined with uneven traffic per client turns
your "load balanced" system into an accidentally unbalanced one — one
heavy client's traffic all lands on one server. If session affinity is
required, pair it with a session store (Redis, etc.) so any server can
serve any session, instead of hard-pinning by IP.

## What we'd do differently

*(Fill this in with a real story once you've shipped this in production —
this section is what separates the post from a textbook definition.)*

---

**Round robin, least connections, or something custom — what have you
actually run in production, and what forced the choice?**

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
