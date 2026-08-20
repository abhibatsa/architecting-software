# Caching patterns & invalidation

**Read time:** 3 min

---

There are only two hard problems in computer science: cache invalidation,
naming things, and off-by-one errors. The joke lands because it's true —
caching itself is easy. Knowing when a cached value is wrong is the actual
skill.

## The core patterns

**Cache-aside (lazy loading):** application checks cache first, on a miss
reads from the database and populates the cache. Most common pattern —
simple, and only caches what's actually requested. Downside: the first
request after a miss is always slow, and a cache-wide flush causes a
"thundering herd" of simultaneous DB reads.

**Write-through:** every write goes to the cache and the database
together, synchronously. Cache is never stale, but every write pays the
latency cost of both operations.

**Write-behind (write-back):** writes go to the cache immediately, and get
flushed to the database asynchronously in the background. Fast writes, but
a real risk: if the cache node dies before the flush happens, that write
is gone.

## Invalidation strategies

- **TTL (time-to-live):** simplest option — cached values expire after a
  fixed window. Accepts some staleness in exchange for simplicity.
- **Explicit invalidation on write:** the write path actively deletes or
  updates the cached entry. More accurate, more code paths to get right —
  miss one write path and you have silently stale data with no expiry to
  save you.
- **Event-driven invalidation:** a change event (e.g. from a database
  change stream or message queue) triggers cache invalidation
  downstream, decoupling the writer from needing to know about every
  cache that might hold the value.

## The part most people get wrong

Choosing a TTL isn't a technical decision made in isolation — it's a
business decision about acceptable staleness, and it should be set per
data type, not globally. A product price can tolerate a 5-minute-stale
cache. A user's account balance cannot. Treating cache TTL as one global
config value is a common design smell — it means someone picked a number
that's simultaneously too aggressive for slow-changing data and too loose
for fast-changing data.

## Cache eviction, briefly

When the cache is full, something has to go. LRU (least recently used) is
the default most systems reach for — but for access patterns with strong
recency bias broken by occasional big scans (a full-table batch job, for
example), LRU can evict genuinely hot data during that scan. LFU (least
frequently used) or a hybrid (like LRU with a frequency-aware admission
policy) handles that case better, at the cost of more bookkeeping.

## What we'd do differently

*ToDo*

---

**What's the worst stale-cache bug you've shipped?** Open an issue or drop
a comment on the video.

*Part of [System Design & Architecture](../README.md) → [Core Concepts](./README.md)*
