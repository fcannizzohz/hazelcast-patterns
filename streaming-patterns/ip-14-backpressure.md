[Patterns](../patterns.md) › [Streaming patterns](README.md) › [Production concerns at the boundaries](README.md#production-concerns-at-the-boundaries)

# IP-14 Backpressure

**Intent.** A slow stage throttles the stages before it, up to the source.

**Context.** One stage of a pipeline is slower than the rest.

**Problem.** How do you stop a slow stage from filling intermediate queues and overwhelming the system?

**Forces.**
- External producers do not slow down on their own.
- Buffering everything eventually runs out of memory or drops events.

**Solution.** Let the slow stage push back on the stages before it, so the pipeline consumes less at the source. Across journal-chained jobs, use metrics from later stages to throttle the first stage, so the whole system consumes less at its boundary.

**Structure.**

```mermaid
flowchart LR
    K[[Durable log]] --> S1[Stage 1] --> S2[Stage 2] --> S3[Slow stage 3]
    S3 -. backpressure .-> S2
    S2 -. backpressure .-> S1
    S1 -. "consume less" .-> K
```

**Hazelcast mechanics.** Within one job, Jet propagates backpressure through the DAG automatically, across members too, using bounded queues and flow control. A map journal does not push back on the stage that writes to it; it overwrites old events instead ([IP-13](ip-13-lost-journal-recovery.md)). Between separate jobs there is no built-in throttling: write it yourself, for example a source that slows down based on job metrics or on journal lag.

**Consequences.**
- (+) Overload is absorbed at the boundary, where a durable log can hold it. Sources that cannot be paused (for example non-durable push sources) still lose or buffer data.
- (−) Ingestion lag grows during overload.

**Related patterns.** [IP-8](ip-08-journal-chained-stages.md), [IP-13](ip-13-lost-journal-recovery.md), [IP-16](ip-16-async-batched-io.md).

---

← [IP-13 Lost Journal Recovery](ip-13-lost-journal-recovery.md) · [IP-16 Async Batched I/O](ip-16-async-batched-io.md) →
