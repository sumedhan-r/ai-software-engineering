# Docs index

<!-- One line per doc: what it covers and when to read it.
     Agents use this to load only what a task needs. -->

## Principles (conceptual)

| Doc | Read when |
| --- | --- |
| [design-philosophy.md](principles/design-philosophy.md) |  |
| [observability.md](principles/observability.md) | Adding or changing logging, tracing, metrics or alerts. Deeper notes in [observability/](principles/observability/). |
| [refactoring.md](principles/refactoring.md) |  |

## Guides (instructional)

| Doc | Read when |
| --- | --- |
| [api.md](guides/api.md) |  |
| [schemas.md](guides/schemas.md) |  |
| [repository.md](guides/repository.md) |  |
| [service-layer.md](guides/service-layer.md) |  |
| [testing.md](guides/testing.md) |  |
| [infra.md](guides/infra.md) |  |

## Decisions

One file per decision, numbered in order (`0001-short-title.md`). Each records why one option was chosen over others, so neither you nor an agent re-argues it later. Copy [decision-template.md](decisions/decision-template.md) to start one.

## Specs

See [specs/](specs/). A product starts from [product-brief-template.md](specs/product-brief-template.md), owned by the requester: the goal, deliverables and habits it should build. The developer turns it into [guardrails-template.md](specs/guardrails-template.md): intent, design and layout, behaviours, boundaries and dependability rules, checked at every stage from spec to operations. Each feature then gets a [feature-spec-template.md](specs/feature-spec-template.md), then a [tech-spec-template.md](specs/tech-spec-template.md).

Check a product's guardrails at each stage, using its "When to check" table. Read its brief only when a spec leaves the goal or a deliverable unclear.
