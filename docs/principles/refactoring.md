# Refactoring

Agent: read this before restructuring existing code, removing duplication, or moving logic between modules. Rules for what the result should look like are in [design-philosophy.md](design-philosophy.md).

---

## Rules

**REF-1 — Remove code drift by extracting only the identical part.**
Rule: when the same logic appears in two or more places, extract it into one function that meets DP-4, and leave caller-specific differences at each caller. If the extraction can't meet DP-4, keep the duplication and add a comment explaining why.
Why: drifted copies diverge over time. A bug fixed in one copy stays live in the others.
In code: a diff that changes logic in one place while an identical copy elsewhere stays unchanged is a drift signal and should be flagged.

---

## Don't

- Do not merge logic that is only similar into one function with flags to cover the differences.
