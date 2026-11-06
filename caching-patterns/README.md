[Patterns](../patterns.md) › Caching patterns

# Caching patterns

How applications read and write data through Hazelcast as a cache in front of a system of record.

Patterns IP-1 to IP-6 choose how reads and writes flow between application, cache and store. The later patterns deal with what goes wrong in those flows: stale or resurrected values, load spikes, freshness, and persistence failures. IDs are not contiguous because IP-7 to IP-18 are streaming patterns.

## Access patterns

How the application, the cache and the system of record divide reads and writes.

| ID | Pattern | Intent |
|---|---|---|
| IP-1 | [Cache-Aside](ip-01-cache-aside.md) | Application manages the cache itself |
| IP-2 | [Read-Through](ip-02-read-through.md) | Cache loads missing entries from the store |
| IP-3 | [Write-Through](ip-03-write-through.md) | Cache writes to the store synchronously |
| IP-4 | [Write-Behind](ip-04-write-behind.md) | Cache writes to the store asynchronously |
| IP-5 | [Refresh-Ahead](ip-05-refresh-ahead.md) | Cache is updated before clients ask |
| IP-6 | [Near-Cache](ip-06-near-cache.md) | Client keeps a local copy of hot entries |

## Invalidation and stale data

How to keep absent, deleted and superseded values from being served.

| ID | Pattern | Intent |
|---|---|---|
| IP-19 | [Negative Caching](ip-19-negative-caching.md) | Remember confirmed absence for a short time |
| IP-20 | [Tombstone with Version Guard](ip-20-tombstone-with-version-guard.md) | Deletes and newer versions win over late writes |
| IP-21 | [Query-Result Cache with Generation-Based Invalidation](ip-21-query-result-cache-with-generation-invalidation.md) | Invalidate many cached queries by moving a scope's generation |
| IP-22 | [Stale-Fill Prevention with Load Tokens](ip-22-stale-fill-prevention-with-load-tokens.md) | A late load cannot undo an invalidation |

## Load and freshness

How to control load on the store and how old a served value may be.

| ID | Pattern | Intent |
|---|---|---|
| IP-23 | [Miss Coalescing](ip-23-miss-coalescing.md) | Concurrent misses on a key load it once |
| IP-24 | [Freshness Separate from TTL](ip-24-freshness-separate-from-ttl.md) | Data age decides freshness; TTL only decides retention |
| IP-25 | [Selective Warm-Up](ip-25-selective-warm-up.md) | Preload the hot set at a controlled rate |

## Persistence safety

How to persist from the cache without losing or corrupting data.

| ID | Pattern | Intent |
|---|---|---|
| IP-26 | [Retry-Safe MapStore Batches](ip-26-retry-safe-mapstore-batches.md) | Repeated and partly failed writes stay correct |
| IP-27 | [Write-Behind Loss Budget and Recovery](ip-27-write-behind-loss-budget-and-recovery.md) | Keep unpersisted data within an explicit budget |
