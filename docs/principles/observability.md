# Observability Engineering

Agent: read this before adding or changing any logging, tracing, metrics, or alerts. Deeper notes are linked at the bottom.

---

## Rules

**OBS-1 — Emit one wide structured event per unit of work.**
Rule: each request, job, or handler produces a single event with all context fields attached at the end of execution.
Why: aggregating narrow events after the fact destroys the correlation needed for root cause analysis.
In code: a diff that adds a second `log.info(...)` inside the same handler probably violates this — consolidate into one event.

**OBS-2 — Include high-cardinality fields on every event.**
Rule: every event carries `user_id`, `request_id`, `feature`, `service`, and `environment` at minimum.
Why: slicing on low-cardinality fields (status code, endpoint) cannot isolate one user's failure path.
In code: no log call is acceptable without these fields attached to the logger or span context beforehand.

**OBS-3 — Classify every error as business or downstream.**
Rule: every error event has an `error_type` field set to `business` (expected, rules violation) or `downstream` (dependency, network, timeout).
Why: HTTP status codes and exception names cannot distinguish the two; mixing them makes alert thresholds meaningless.
In code: an exception handler that sets only `exc_info=True` without `error_type` fails this rule.

**OBS-4 — Propagate a trace ID across every boundary.**
Rule: a single `trace_id` must appear on every event for a given request, including outbound calls to other services, database queries, and background tasks spawned from that request.
Why: incidents in distributed systems rarely have a single source; the trail of breadcrumbs across components is the only reliable path to root cause.
In code: any HTTP client call or task dispatch that does not forward the current trace context header fails this rule.

**OBS-5 — Define alerts from user experience, not infrastructure.**
Rule: alert thresholds are set against SLOs (error rate, latency percentiles at the feature level), not against CPU, memory, or pod count.
Why: a container can be at 90 % CPU while the user experience is fine, and vice versa.
In code: a new alert configured on a raw infrastructure metric requires a written justification that no SLO covers the failure mode.

**OBS-6 — Instrument at the Traits and Behaviors boundary.**
Rule: before adding instrumentation to a unit of work, write down its Traits (what it holds: connection pool, retry config, lock table) and its Behaviors (input → processing → output). Instrument to confirm those Behaviors at runtime.
Why: instrumentation without a prior model of what is expected produces noise; you cannot detect an anomaly if you never stated the norm.
In code: spans and events on a class that has no documented Behaviors in the spec are a signal the instrumentation is speculative.

---

## Don't

- Do not use plain-text log strings. Structured key-value fields are required.
- Do not aggregate before storing (pre-bucketed histograms, sampled-down event counts). Store raw events; aggregate at query time.
- Do not reuse the same `trace_id` across logically separate requests, even if they share a session.
- Do not instrument infrastructure components in isolation without linking events back to the originating request.
- Do not set an alert without a runbook entry describing what the alert means and the first response action.

---

## Deeper notes

| File | Read when |
| --- | --- |
| [01_foundation.md](observability/01_foundation.md) | You need background on why monitoring is insufficient for distributed systems, or the definitions of cardinality and dimensionality. |
| [02_telemetry.md](observability/02_telemetry.md) | You are choosing between structured events, metrics, and traces, or working with OpenTelemetry configuration. |
