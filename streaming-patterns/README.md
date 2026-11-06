[Patterns](../patterns.md) › Streaming patterns

# Streaming patterns

How streaming pipelines connect to each other and to external systems, and how they cope with overload, duplicates, slow dependencies and failure.

## Pipeline composition and data contracts

These patterns describe how streaming pipelines connect to each other and to their inputs and outputs, in an online event-processing system built as several stages.

| ID | Pattern | Intent |
|---|---|---|
| IP-7 | [Template Jobs](ip-07-template-jobs.md) | Reusable pipeline parts composed by service teams |
| IP-8 | [Journal-Chained Stages](ip-08-journal-chained-stages.md) | Each stage's output map triggers the next stage |
| IP-9 | [Data as Contract](ip-09-data-as-contract.md) | A shared schema decouples pipelines |
| IP-10 | [Fan-in / Fan-out](ip-10-fan-in-fan-out.md) | Split, correlate and re-assemble streams |
| IP-11 | [Enrichment Pipeline](ip-11-enrichment-pipeline.md) | Look up in-memory reference data per event |
| IP-12 | [Durable Maps](ip-12-durable-maps.md) | Persist pipeline state to the system of record |

## Production concerns at the boundaries

These patterns deal with overload, duplicates, slow dependencies and failure where pipelines meet the outside world, including legacy systems that are not idempotent.

| ID | Pattern | Intent |
|---|---|---|
| IP-13 | [Lost Journal Recovery](ip-13-lost-journal-recovery.md) | Detect and recover events a journal dropped |
| IP-14 | [Backpressure](ip-14-backpressure.md) | Slow stages throttle the source |
| IP-16 | [Async Batched I/O](ip-16-async-batched-io.md) | Call slow services in asynchronous batches |
| IP-17 | [Processing Guarantee](ip-17-processing-guarantee.md) | At-least-once or exactly-once per pipeline |
| IP-18 | [Partitioned Compute](ip-18-partitioned-compute.md) | Process each event where its data lives |

IP-15 (Dedup with Flush on Snapshot) was removed on 6 November 2026 and its ID is retired. For exactly-once effects, see [IP-17](ip-17-processing-guarantee.md) and [ARCH-5](../architecture-patterns/arch-05-platform-level-idempotency.md).
