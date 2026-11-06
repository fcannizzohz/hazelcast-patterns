[Patterns](../patterns.md) › Solution patterns

# Solution patterns

End-to-end solutions to a recognisable business problem, described as concepts. Each solution names the problem it solves, the idea behind it, the existing caching, streaming and architecture patterns it is built from, and the limits of its guarantees.

A solution pattern sits above the other categories. A caching or streaming pattern answers one design question; an architecture pattern gives the shape of a system or a capability; a solution pattern combines several of them, plus some logic of its own, into something a team can adopt as a whole. Solutions are still technology-neutral templates: Hazelcast specifics appear only in **Hazelcast mechanics**, at the level of features.

Each solution here started as a proof of concept or a design study. Where a page quotes measurements, they come from that study and hold only for its workload; they are evidence for the mechanism, not a production target.

| ID | Solution | Intent |
|---|---|---|
| SOL-1 | [Semantic Relational Cache](sol-01-semantic-relational-cache.md) | Answer whole predicate queries from the cache when it can prove it holds every matching row, and fetch only the missing part otherwise |
| SOL-2 | [High-Throughput Tiered Idempotency](sol-02-high-throughput-tiered-idempotency.md) | Skip the durable duplicate check for keys an in-memory filter proves new, while an atomic claim keeps duplicates out |
| SOL-3 | [Read Tier for Ephemeral Clients](sol-03-read-tier-for-ephemeral-clients.md) | Long-lived read nodes cache immutable data so short-lived processes stop re-reading it from the cluster |
