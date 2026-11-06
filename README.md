# Hazelcast patterns

A catalogue of patterns for building systems with Hazelcast, from basic cache access to stream-processing pipelines and platform-level capabilities.

The first patterns target systems that use Hazelcast as a hot-data and stream-processing layer in front of one or more systems of record. They are domain-neutral: they apply to orders, transactions, events, sessions, devices or any other entity that is read, updated and processed at high rate. The system of record stays authoritative; Hazelcast holds a hot copy.

**Start here: [patterns.md](patterns.md)** lists every pattern, grouped by category.

## How the repository is organised

Each category of patterns has its own directory. Inside it, a `README.md` introduces the category and lists its patterns, and each pattern lives in its own Markdown file.

```
.
├── README.md                    this file
├── patterns.md                  catalogue of all patterns, by category
├── glossary.md                  terms used across the patterns
├── CONTRIBUTING.md              how to add a pattern or a category
├── templates/
│   ├── pattern-template.md      skeleton for a new pattern
│   └── solution-template.md     skeleton for a new solution pattern
├── caching-patterns/            IP-1 to IP-6, IP-19 to IP-27: reading and writing through Hazelcast as a cache
│   ├── README.md
│   └── ip-01-cache-aside.md …
├── streaming-patterns/          IP-7 to IP-18: composing pipelines and handling production concerns at their boundaries
│   ├── README.md
│   └── ip-07-template-jobs.md …
├── architecture-patterns/       ARCH-n: system-level and capability architectures
│   ├── README.md
│   ├── arch-01-operational-data-fabric.md …
│   └── arch-05-platform-level-idempotency.md …
└── solution-patterns/           SOL-n: end-to-end solutions described as concepts
    ├── README.md
    └── sol-01-semantic-relational-cache.md …
```

New categories will be added over time as new top-level directories, each with its own ID prefix. Caching and streaming patterns share the IP prefix because they started as one integration category; their IDs were kept so existing references stay valid. Architecture patterns use ARCH only; the IMP patterns of the former implementation category were renumbered ARCH-5 to ARCH-11. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Categories

| Category | Prefix | What it covers |
|---|---|---|
| [Caching patterns](caching-patterns/README.md) | IP | How applications read and write data through Hazelcast as a cache in front of a system of record. |
| [Streaming patterns](streaming-patterns/README.md) | IP | How streaming pipelines connect to each other and to external systems, and how they cope with overload, duplicates, slow dependencies and failure. |
| [Architecture patterns](architecture-patterns/README.md) | ARCH | System-level and capability architectures built on Hazelcast, combining the caching and streaming patterns. |
| [Solution patterns](solution-patterns/README.md) | SOL | End-to-end solutions to a recognisable business problem, described as concepts and composed from the other patterns. |

## Editions

The patterns are not tied to a Hazelcast version. Features that need Hazelcast Enterprise are marked as such in each pattern, among them the CP Subsystem and `CPMap`, the current CDC connectors, WAN replication and the Kubernetes Operator.

## How to read a pattern

Every pattern uses the same structure:

Every pattern uses the same structure:

| Section | Meaning |
|---|---|
| **Intent** | One line on what the pattern does. |
| **Context** | The situation in which the pattern applies. |
| **Problem** | The question the pattern answers. |
| **Forces** | The pressures that pull against each other. |
| **Solution** | What to do. |
| **Structure** | A diagram of the participants and the flow. |
| **Hazelcast mechanics** | The Hazelcast features that implement it. |
| **Consequences** | What you gain (+) and what you pay (−). |
| **Related patterns** | Links to related patterns, in this or other categories. |

Pattern IDs (for example IP-4 or ARCH-5) are stable and are used for cross-references. Diagrams are written in [Mermaid](https://mermaid.js.org/), which GitHub renders inline.

Hazelcast terms such as member, partition, IMap, map journal and CP Subsystem are defined in the [glossary](glossary.md).
