[Patterns](../patterns.md) › Architecture patterns

# Architecture patterns

System-level and capability architectures built on Hazelcast, combining the caching and streaming patterns.

The TEV model's seven blueprints map onto this category: Operational Data Fabric, Brownout and Degraded Mode, Burst Absorption and Compute Near Data are ARCH-1 to ARCH-4; Read Acceleration is [ARCH-7](arch-07-shared-reference-map-with-near-cache.md) and [ARCH-8](arch-08-change-fed-read-model.md); Control Plane Consistency is [ARCH-5](arch-05-platform-level-idempotency.md) and [ARCH-6](arch-06-site-strategy-per-data-class.md); Streaming Materialised View is [ARCH-10](arch-10-live-operational-view.md).

See [ID history](#id-history) for the former IMP IDs of ARCH-5 to ARCH-11.

## System architectures

Patterns that combine several caching, streaming and capability patterns to solve a class of business problem. ARCH-1 to ARCH-4 come from the TEV model's blueprints.

| ID | Pattern | Intent |
|---|---|---|
| ARCH-1 | [Operational Data Fabric](arch-01-operational-data-fabric.md) | One read layer over several systems of record that keep ownership |
| ARCH-2 | [Brownout and Degraded Mode](arch-02-brownout-and-degraded-mode.md) | Keep critical journeys working when load or dependencies fail |
| ARCH-3 | [Burst Absorption](arch-03-burst-absorption.md) | A bounded buffer smooths spikes for a constrained consumer |
| ARCH-4 | [Compute Near Data](arch-04-compute-near-data.md) | Ship processing to the data, return only results |

## Capability architectures

Reusable architectures for one capability each (idempotency, site resilience, read offload, elastic state, live views, migration, process coordination, filtered subscriptions, request-reply), built from Hazelcast's building blocks. The system of record stays authoritative throughout.

| ID | Pattern | Intent |
|---|---|---|
| ARCH-5 | [Platform-Level Idempotency](arch-05-platform-level-idempotency.md) | Claim each operation's key once, atomically |
| ARCH-6 | [Site Strategy per Data Class](arch-06-site-strategy-per-data-class.md) | Each data class gets its own resilience strategy |
| ARCH-7 | [Shared Reference Map with Near Cache](arch-07-shared-reference-map-with-near-cache.md) | Serve reference data from memory |
| ARCH-8 | [Change-Fed Read Model](arch-08-change-fed-read-model.md) | CDC-fed copy offloads reads from the store; also serves migrations |
| ARCH-9 | [State Externalisation with In-Place Updates](arch-09-state-externalisation-with-in-place-updates.md) | Move service state into the grid, update in place |
| ARCH-10 | [Live Operational View](arch-10-live-operational-view.md) | Streaming job maintains live views and totals |
| ARCH-11 | [Orchestration as Dataflow](arch-11-orchestration-as-dataflow.md) | Replace chatty service calls with a DAG |
| ARCH-12 | [Process Manager with Keyed State](arch-12-process-manager-with-keyed-state.md) | Drive each process instance as one keyed record, with time-outs |
| ARCH-13 | [Server-Side Filtered Subscriptions](arch-13-server-side-filtered-subscriptions.md) | Push only matching changes; keep a local matching copy |
| ARCH-14 | [Request-Reply over the Grid](arch-14-request-reply-over-the-grid.md) | Async request and reply by correlation id through maps |

## Combining patterns

- **Read acceleration with degraded mode.** A copy of the data adds resilience only when the system is designed to serve from it while the source is down ([ARCH-2](arch-02-brownout-and-degraded-mode.md) with [ARCH-8](arch-08-change-fed-read-model.md)). Without that design, a miss still reaches the failed source.
- **Live views with compute near data.** Live views ([ARCH-10](arch-10-live-operational-view.md)) can be queried and aggregated where they are held ([ARCH-4](arch-04-compute-near-data.md)).
- **Data fabric with read acceleration.** An operational data layer ([ARCH-1](arch-01-operational-data-fabric.md)) is fed the same way as a change-fed read model ([ARCH-8](arch-08-change-fed-read-model.md)), with Near Cache for hot reference data ([ARCH-7](arch-07-shared-reference-map-with-near-cache.md)).
- **Strong consistency with burst absorption.** CP claims ([ARCH-5](arch-05-platform-level-idempotency.md)) have bounded throughput per Raft group, so at burst rate they belong after the buffer ([ARCH-3](arch-03-burst-absorption.md)), not in front of it.

## ID history

The capability architectures came from the former implementation-patterns category with the prefix IMP and were renumbered to ARCH on 2026-11-06. Older notes, including the review logs, use the old IDs.

| Old ID | New ID |
|---|---|
| IMP-1 | ARCH-5 |
| IMP-2 | ARCH-6 |
| IMP-3 | ARCH-7 |
| IMP-4 | ARCH-8 |
| IMP-5 | ARCH-9 |
| IMP-6 | ARCH-10 |
| IMP-7 | Retired: Coexistence View was merged into IMP-4, now ARCH-8, as its migration variant |
| IMP-8 | ARCH-11 |
