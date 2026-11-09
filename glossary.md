[Patterns](patterns.md) › Glossary

# Glossary

Terms used across the patterns.

| Term | Meaning |
|---|---|
| **Member** | A Hazelcast cluster node. Data is split into partitions (271 by default); each partition has an owner member and one or more backups on other members. |
| **Client** | An application process connected to the cluster. A smart client knows which member owns each partition and sends each key operation straight to it. |
| **IMap** | Hazelcast's distributed, partitioned key-value map. |
| **Near Cache** | A client-side (or member-side) local copy of map entries, kept up to date by asynchronous invalidations from the cluster, so it is eventually consistent. |
| **ReplicatedMap** | A map fully copied to every member, updated asynchronously; eventually consistent. |
| **Write-behind / write coalescing** | Write-behind persists changes to the store asynchronously, after a delay. With coalescing, only the latest value of each key in the queue is written. |
| **CDC (change data capture)** | Reading a database's change log so that inserts, updates and deletes become a stream of events. |
| **Compact serialisation** | Hazelcast's schema-based serialisation format, which allows fields to be added and removed between versions of a class. |
| **Tombstone** | A record that marks a key as deleted, kept for a while so that late or replayed writes cannot bring the key back. |
| **Miss coalescing (single-flight)** | Letting only one load per key run at a time, with concurrent callers waiting for its result. |
| **MapLoader / MapStore** | Interfaces through which an IMap reads from and writes to an external data store. |
| **Map journal** | The event journal of an IMap: a partitioned, fixed-capacity, in-memory ring buffer of changes that pipelines can consume. Its capacity is the total for the map, split evenly across partitions; when full, the oldest events are overwritten. |
| **Pipeline / Job** | A stream-processing graph (DAG) of sources, stages and sinks, run as a job on every member, next to the data. |
| **Snapshot** | A periodic, consistent checkpoint of a job's internal state and source offsets, used to restart it after a failure. Snapshots are stored in the cluster's memory; data the job has already written to IMaps or external sinks is not part of it. |
| **CP Subsystem** | Hazelcast's strongly consistent subsystem, built on Raft groups of 3 to 7 members. Provides `FencedLock`, `IAtomicLong`, `ISemaphore`, `CPMap` and other structures. It must be enabled (`cp-member-count` of at least 3); otherwise the CP structures run in "unsafe mode" without strong consistency. Enterprise Edition. |
| **AP / CP** | AP structures (IMap, ReplicatedMap, and others) stay available during a network split and may diverge, then merge by policy. CP structures stay consistent and stop serving on the minority side. |
| **Split-brain protection** | A per-structure minimum cluster size; below it, operations are rejected. It narrows the window in which both sides of a split accept writes, but only takes effect once the split is detected, which depends on the failure detector (by default a member is declared dead after 60 seconds without a heartbeat, `hazelcast.max.no.heartbeat.seconds`). |
| **System of record** | The authoritative store (relational database, NoSQL store, ledger). Hazelcast holds a hot copy; the system of record stays authoritative. |
| **Entry processor** | Code sent to the member that owns a key and run there on the key's partition thread, atomically for that key. |
| **Brownout / degraded mode** | Brownout: switching off optional work under overload. Degraded mode: continuing with reduced function when a dependency fails. |
| **Ringbuffer** | A fixed-capacity, in-memory ring of items held in one partition; old items are overwritten when it is full (or the writer is refused, depending on settings). |
| **Reliable Topic** | A publish-subscribe topic backed by a Ringbuffer, so listeners can catch up on recent messages; retention is bounded by the ring. |
| **`ReliableMessageListener`** | A Reliable Topic listener that can choose its starting sequence, store the last one it processed, and declare whether it tolerates lost messages. |
| **`TopicOverloadPolicy`** | What a Reliable Topic publisher does when the ring is full of unexpired messages: block, fail, or discard the newest or oldest. |
| **Continuous Query Cache** | A client- or member-side copy of the entries of a map that match a predicate, kept current by events; eventually consistent. |
| **Suspend on failure** | A job setting: on an error the job is suspended, keeping its snapshot so it can be resumed, instead of being terminated. |
| **Preserve order** | A pipeline setting that stops events being reordered between parallel processors; it keeps the source's order per partition, not a total order. |
