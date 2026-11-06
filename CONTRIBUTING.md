# Contributing

## Adding a pattern to an existing category

1. Copy [templates/pattern-template.md](templates/pattern-template.md) into the category directory.
2. Give it the next free ID in that category and name the file `<prefix>-<nn>-<pattern-name>.md`, with a two-digit number and a lowercase, hyphenated name. For example `ip-28-read-replica.md`.
3. Fill in every section of the template. Keep it domain-neutral.
4. Link related patterns by ID with relative links, such as `[IP-2](ip-02-read-through.md)` in the same category or `[ARCH-7](../architecture-patterns/arch-07-shared-reference-map-with-near-cache.md)` across categories.
5. Add a row to the category's `README.md` and to [patterns.md](patterns.md).
6. Update the previous/next links at the bottom of the neighbouring pattern files.

Keep implementation details out of the pattern: Intent, Context, Problem, Forces, Solution and Structure stay technology-neutral, and Hazelcast specifics go only in **Hazelcast mechanics**, named at the level of features and APIs. Code, configuration files and database-specific SQL belong in examples, not in the pattern.
7. Add any new Hazelcast term to [glossary.md](glossary.md).
8. State the guarantee honestly: say whether a structure is AP or CP, what happens on member loss and split-brain, and which features need Enterprise Edition.

IDs are permanent. If a pattern is retired, keep its ID unused rather than renumbering the others, so existing links and references stay valid.

## Adding a category

1. Create a top-level directory named after the category, in lowercase with hyphens, for example `security-patterns/`.
2. Pick a short ID prefix that no other category uses, for example `SEC`. (Caching patterns keep `IP`, the prefix of the category they started in. Former IDs were renumbered on 2026-11-06: streaming patterns from `IP` to `STR`, see the [streaming README](streaming-patterns/README.md#id-history), and `IMP` patterns to `ARCH`, see the [architecture README](architecture-patterns/README.md#id-history). Retired IDs are never reused.)
3. Add a `README.md` to the directory with a breadcrumb back to [patterns.md](patterns.md), a short introduction, and a table of the category's patterns (optionally grouped into sections).
4. Add the category to the table in the root [README.md](README.md), to the directory tree there, and as a new section in [patterns.md](patterns.md).

## Solution patterns

A solution pattern uses [templates/solution-template.md](templates/solution-template.md). It adds four sections to the pattern template: **Composed of** (the patterns it builds on, each with its role), **Consistency limits** (what the guarantees do not cover), **When not to use it**, and **Background** (sources). Measurements from a proof of concept are quoted only with their conditions.

## Conventions

- One pattern per file; one category per directory.
- Diagrams in Mermaid code blocks.
- Every pattern page starts with a breadcrumb line and ends with previous/next links.
