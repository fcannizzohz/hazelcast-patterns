[Patterns](../patterns.md) › Streaming patterns

# Streaming patterns

How streaming pipelines connect to each other and to external systems, and how they cope with overload, duplicates, slow dependencies and failure.

## Pipeline composition and data contracts

These patterns describe how streaming pipelines connect to each other and to their inputs and outputs, in an online event-processing system built as several stages.

| ID | Pattern | Intent |
|---|---|---|
| STR-1 | [Template Jobs](str-01-template-jobs.md) | Reusable pipeline parts composed by service teams |
| STR-2 | [Journal-Chained Stages](str-02-journal-chained-stages.md) | Each stage's output map triggers the next stage |
| STR-3 | [Data as Contract](str-03-data-as-contract.md) | A shared schema decouples pipelines |
| STR-4 | [Fan-in / Fan-out](str-04-fan-in-fan-out.md) | Split, correlate and re-assemble streams |
| STR-5 | [Enrichment Pipeline](str-05-enrichment-pipeline.md) | Look up in-memory reference data per event |
| STR-6 | [Durable Maps](str-06-durable-maps.md) | Persist pipeline state to the system of record |

## Production concerns at the boundaries

These patterns deal with overload, duplicates, slow dependencies and failure where pipelines meet the outside world, including legacy systems that are not idempotent.

| ID | Pattern | Intent |
|---|---|---|
| STR-7 | [Lost Journal Recovery](str-07-lost-journal-recovery.md) | Detect and recover events a journal dropped |
| STR-8 | [Backpressure](str-08-backpressure.md) | Slow stages throttle the source |
| STR-9 | [Async Batched I/O](str-09-async-batched-io.md) | Call slow services in asynchronous batches |
| STR-10 | [Processing Guarantee](str-10-processing-guarantee.md) | At-least-once or exactly-once per pipeline |
| STR-11 | [Partitioned Compute](str-11-partitioned-compute.md) | Process each event where its data lives |

Dedup with Flush on Snapshot (old ID IP-15) was removed on 6 November 2026 and was never given a STR ID. For exactly-once effects, see [STR-10](str-10-processing-guarantee.md) and [ARCH-5](../architecture-patterns/arch-05-platform-level-idempotency.md).

## ID history

The streaming patterns were split from one integration category with the caching patterns and first used the prefix IP. They were renumbered to STR on 2026-11-06. Older notes use the old IDs.

| Old ID | New ID |
|---|---|
| IP-7 | STR-1 |
| IP-8 | STR-2 |
| IP-9 | STR-3 |
| IP-10 | STR-4 |
| IP-11 | STR-5 |
| IP-12 | STR-6 |
| IP-13 | STR-7 |
| IP-14 | STR-8 |
| IP-15 | Retired: Dedup with Flush on Snapshot, removed |
| IP-16 | STR-9 |
| IP-17 | STR-10 |
| IP-18 | STR-11 |
