[Patterns](../patterns.md) › [Streaming patterns](README.md) › [Pipeline composition and data contracts](README.md#pipeline-composition-and-data-contracts)

# IP-9 Data as Contract

**Intent.** A shared schema lets pipelines evolve independently.

**Context.** Independent teams build pipelines that exchange the same messages.

**Problem.** How do you let pipelines change without breaking each other?

**Forces.**
- Parallel development needs a stable interface.
- Message formats change over time.
- A schema can be specific to one flow or canonical across flows.

**Solution.** Use a schema as the contract between stages, preferably an industry or canonical schema, and a serialisation format that supports schema evolution.

**Structure.**

```mermaid
flowchart LR
    SC{{Shared schema contract}}
    TA[Team A pipeline v1] -->|writes| M[(Shared map)]
    M -->|reads| TB[Team B pipeline v2]
    SC -.-> TA
    SC -.-> TB
```

**Hazelcast mechanics.** Compact serialisation. It supports adding and removing fields between versions; readers must check whether an optional field exists (`GenericRecord.getFieldKind` or the reader's `getFieldKind`) before reading it. Changing a field's type is not a compatible change. Schemas are replicated by the cluster itself, so no external schema registry is needed inside Hazelcast. On Kafka edges, the usual choice is Avro or Protobuf with a schema registry.

**Consequences.**
- (+) Pipelines can be developed and deployed independently.
- (+) Every stage can evolve on its own.
- (−) Compatibility rules must be agreed and enforced; nothing in Hazelcast rejects an incompatible change at write time.

**Related patterns.** [IP-7](ip-07-template-jobs.md), [IP-8](ip-08-journal-chained-stages.md).

---

← [IP-8 Journal-Chained Stages](ip-08-journal-chained-stages.md) · [IP-10 Fan-in / Fan-out](ip-10-fan-in-fan-out.md) →
