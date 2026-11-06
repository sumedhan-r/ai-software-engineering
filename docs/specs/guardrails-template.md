# Guardrails: <product>

- Owner: <!-- developer -->
- Brief: <!-- link to product brief -->

<!-- Owned and kept current by the developer. Short, checkable rules: each one
     should be something a spec or a diff can be checked against.
     Changing or removing a rule goes through a PR; reversing one gets a
     decision record. -->

## When to check

<!-- Each stage reads only the sections it needs. A gap found at any stage
     becomes a new rule here, so the next pass catches it. -->

| Stage | Check | Feeds back |
| --- | --- | --- |
| Feature spec | Intent, Behaviours | A conflict with a rule, or a new behaviour to add |
| Tech spec | Design and layout, Boundaries, Dependability | A boundary or contract change, a new signal or failure mode |
| Coding and review | All sections | Rule IDs touched, listed in the PR |
| Operating (incidents, alerts, SLO misses) | Dependability, Behaviours | A rule that would have caught it |

## Intent

<!-- What this product optimises for, and what it will not trade away.
     INT-1: <rule> (why, in one line) -->

## Design and layout

<!-- Where things live: modules, screens, layers, naming.
     LAY-1: <rule> -->

## Behaviours

<!-- What must always hold, whatever the feature. Each one names its test.
     BEH-1: <rule>. Test: <path or name> -->

## Boundaries

<!-- One row per component. "Must not use" is the guardrail. -->

| Component | Owns | May use | Must not use | Contract |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |

## Dependability

<!-- Product-specific targets only; general rules stay in principles/
     (e.g. observability.md, design-philosophy.md). Keep all seven rows:
     write "n/a: <reason>" instead of deleting one, so a skipped attribute
     is a visible choice. Add DEP-n rows under an attribute as needed;
     each names the signal that shows it holds. Specs and reviews check
     only the rows a change touches. -->

| ID | Attribute | Rule | Signal |
| --- | --- | --- | --- |
| DEP-1 | Availability |  |  |
| DEP-2 | Reliability |  |  |
| DEP-3 | Maintainability |  |  |
| DEP-4 | Safety |  |  |
| DEP-5 | Confidentiality |  |  |
| DEP-6 | Integrity |  |  |
| DEP-7 | Observability |  |  |
