# Pattern catalogue

Every pattern in this repository, grouped by category. Each entry links to its own page. See the [README](README.md) for how the catalogue is organised and how to read a pattern.

## [Caching patterns](caching-patterns/README.md)

How applications read and write data through Hazelcast as a cache in front of a system of record.

### Access patterns

| ID | Pattern | Intent |
|---|---|---|
| IP-1 | [Cache-Aside](caching-patterns/ip-01-cache-aside.md) | Application manages the cache itself |
| IP-2 | [Read-Through](caching-patterns/ip-02-read-through.md) | Cache loads missing entries from the store |
| IP-3 | [Write-Through](caching-patterns/ip-03-write-through.md) | Cache writes to the store synchronously |
| IP-4 | [Write-Behind](caching-patterns/ip-04-write-behind.md) | Cache writes to the store asynchronously |
| IP-5 | [Refresh-Ahead](caching-patterns/ip-05-refresh-ahead.md) | Cache is updated before clients ask |
| IP-6 | [Near-Cache](caching-patterns/ip-06-near-cache.md) | Client keeps a local copy of hot entries |

### Invalidation and stale data

| ID | Pattern | Intent |
|---|---|---|
| IP-19 | [Negative Caching](caching-patterns/ip-19-negative-caching.md) | Remember confirmed absence for a short time |
| IP-20 | [Tombstone with Version Guard](caching-patterns/ip-20-tombstone-with-version-guard.md) | Deletes and newer versions win over late writes |
| IP-21 | [Query-Result Cache with Generation-Based Invalidation](caching-patterns/ip-21-query-result-cache-with-generation-invalidation.md) | Invalidate many cached queries by moving a scope's generation |
| IP-22 | [Stale-Fill Prevention with Load Tokens](caching-patterns/ip-22-stale-fill-prevention-with-load-tokens.md) | A late load cannot undo an invalidation |

### Load and freshness

| ID | Pattern | Intent |
|---|---|---|
| IP-23 | [Miss Coalescing](caching-patterns/ip-23-miss-coalescing.md) | Concurrent misses on a key load it once |
| IP-24 | [Freshness Separate from TTL](caching-patterns/ip-24-freshness-separate-from-ttl.md) | Data age decides freshness; TTL only decides retention |
| IP-25 | [Selective Warm-Up](caching-patterns/ip-25-selective-warm-up.md) | Preload the hot set at a controlled rate |

### Persistence safety

| ID | Pattern | Intent |
|---|---|---|
| IP-26 | [Retry-Safe MapStore Batches](caching-patterns/ip-26-retry-safe-mapstore-batches.md) | Repeated and partly failed writes stay correct |
| IP-27 | [Write-Behind Loss Budget and Recovery](caching-patterns/ip-27-write-behind-loss-budget-and-recovery.md) | Keep unpersisted data within an explicit budget |

## [Streaming patterns](streaming-patterns/README.md)

How streaming pipelines connect to each other and to external systems, and how they cope with overload, duplicates, slow dependencies and failure.

### Pipeline composition and data contracts

| ID | Pattern | Intent |
|---|---|---|
| STR-1 | [Template Jobs](streaming-patterns/str-01-template-jobs.md) | Reusable pipeline parts composed by service teams |
| STR-2 | [Journal-Chained Stages](streaming-patterns/str-02-journal-chained-stages.md) | Each stage's output map triggers the next stage |
| STR-3 | [Data as Contract](streaming-patterns/str-03-data-as-contract.md) | A shared schema decouples pipelines |
| STR-4 | [Fan-in / Fan-out](streaming-patterns/str-04-fan-in-fan-out.md) | Split, correlate and re-assemble streams |
| STR-5 | [Enrichment Pipeline](streaming-patterns/str-05-enrichment-pipeline.md) | Look up in-memory reference data per event |
| STR-6 | [Durable Maps](streaming-patterns/str-06-durable-maps.md) | Persist pipeline state to the system of record |

### Production concerns at the boundaries

| ID | Pattern | Intent |
|---|---|---|
| STR-7 | [Lost Journal Recovery](streaming-patterns/str-07-lost-journal-recovery.md) | Detect and recover events a journal dropped |
| STR-8 | [Backpressure](streaming-patterns/str-08-backpressure.md) | Slow stages throttle the source |
| STR-9 | [Async Batched I/O](streaming-patterns/str-09-async-batched-io.md) | Call slow services in asynchronous batches |
| STR-10 | [Processing Guarantee](streaming-patterns/str-10-processing-guarantee.md) | At-least-once or exactly-once per pipeline |
| STR-11 | [Partitioned Compute](streaming-patterns/str-11-partitioned-compute.md) | Process each event where its data lives |

## [Architecture patterns](architecture-patterns/README.md)

System-level and capability architectures built on Hazelcast, combining the caching and streaming patterns.

### System architectures

| ID | Pattern | Intent |
|---|---|---|
| ARCH-1 | [Operational Data Fabric](architecture-patterns/arch-01-operational-data-fabric.md) | One read layer over several systems of record that keep ownership |
| ARCH-2 | [Brownout and Degraded Mode](architecture-patterns/arch-02-brownout-and-degraded-mode.md) | Keep critical journeys working when load or dependencies fail |
| ARCH-3 | [Burst Absorption](architecture-patterns/arch-03-burst-absorption.md) | A bounded buffer smooths spikes for a constrained consumer |
| ARCH-4 | [Compute Near Data](architecture-patterns/arch-04-compute-near-data.md) | Ship processing to the data, return only results |

### Capability architectures

| ID | Pattern | Intent |
|---|---|---|
| ARCH-5 | [Platform-Level Idempotency](architecture-patterns/arch-05-platform-level-idempotency.md) | Claim each operation's key once, atomically |
| ARCH-6 | [Site Strategy per Data Class](architecture-patterns/arch-06-site-strategy-per-data-class.md) | Each data class gets its own resilience strategy |
| ARCH-7 | [Shared Reference Map with Near Cache](architecture-patterns/arch-07-shared-reference-map-with-near-cache.md) | Serve reference data from memory |
| ARCH-8 | [Change-Fed Read Model](architecture-patterns/arch-08-change-fed-read-model.md) | CDC-fed copy offloads reads from the store; also serves migrations |
| ARCH-9 | [State Externalisation with In-Place Updates](architecture-patterns/arch-09-state-externalisation-with-in-place-updates.md) | Move service state into the grid, update in place |
| ARCH-10 | [Live Operational View](architecture-patterns/arch-10-live-operational-view.md) | Streaming job maintains live views and totals |
| ARCH-11 | [Orchestration as Dataflow](architecture-patterns/arch-11-orchestration-as-dataflow.md) | Replace chatty service calls with a DAG |

## [Solution patterns](solution-patterns/README.md)

End-to-end solutions to a recognisable business problem, described as concepts and composed from the other patterns.

| ID | Solution | Intent |
|---|---|---|
| SOL-1 | [Semantic Relational Cache](solution-patterns/sol-01-semantic-relational-cache.md) | Answer whole predicate queries from the cache when it can prove it holds every matching row, and fetch only the missing part otherwise |
| SOL-2 | [High-Throughput Tiered Idempotency](solution-patterns/sol-02-high-throughput-tiered-idempotency.md) | Skip the durable duplicate check for keys an in-memory filter proves new, while an atomic claim keeps duplicates out |
| SOL-3 | [Read Tier for Ephemeral Clients](solution-patterns/sol-03-read-tier-for-ephemeral-clients.md) | Long-lived read nodes cache immutable data so short-lived processes stop re-reading it from the cluster |
