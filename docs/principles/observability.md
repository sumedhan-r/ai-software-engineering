# Observability

<!-- DRAFT: distilled from the notes in observability/. Edit, cut or reword freely.
     Keep only lines you would reject a PR for breaking. -->

Observability is the ability to understand any internal state of the application from its external outputs, without shipping new code to do it. See [foundation](observability/foundation.md#definition).

## Telemetry

- Every unit of work (request, background task, job, pipeline step) emits a wide structured event or span. See [structured events](observability/telemetry.md#structured-events).
- An event captures the unit of work's input, attributes (computed, resolved, discovered), execution conditions and output.
- Every event carries runtime context (container, host, app version, DB version) and request context (user ID, session, headers, query parameters).
- Prefer high-cardinality fields such as user ID and request ID, because they make slicing possible. See [cardinality](observability/foundation.md#cardinality).
- Never store PII or secrets (API keys, user names, emails) in telemetry. Mask before emitting.
- Logs are structured, never free text. See [limitations of logs](observability/telemetry.md#limitations-of-logs).
- Logs, traces and metrics share a correlation context (trace ID, span ID) so they can be joined. See [correlation](observability/telemetry.md#main-design-feature-enabling-observability-for-any-system).
- Record numeric values on the event, not only as pre-aggregated metrics. See [limitations of metrics](observability/telemetry.md#limitations-of-metrics).
- Every external call (database, cache, third-party API) is timed and recorded as its own span.

## Instrumentation

- Use OpenTelemetry. No vendor-specific SDK in application code; exporters are configuration. See [OpenTelemetry](observability/telemetry.md#instrumentation---opentelemetry).
- Rely on auto-instrumentation for API requests and database or cache calls. Add manual spans for business logic. See [auto instrumentation](observability/telemetry.md#auto-instrumentation).
- Instrumentation lives in middleware, decorators or wrappers, not inline in business logic.
- A feature ships with its instrumentation. Observability is never a separate feature added later.

## Monitoring vs observability

- Health is a spectrum, not UP or DOWN. A passing health check does not mean features work. See [limitations to monitoring](observability/overview.md#limitations-to-monitoring).
- Alert on SLOs and user impact, not raw resource thresholds. See [benefits](observability/overview.md#benefits-of-observability).
- Monitor infrastructure metrics only where they correlate with application behavior, and use them to rule infrastructure out first. See [ideal middle ground](observability/telemetry.md#ideal-middle-ground).

## Debugging

- Debug from first principles with the core analysis loop: detect, verify, isolate attributes by diffing baseline and outlier events, repeat. See [core analysis loop](observability/telemetry.md#core-analysis-loop).
- Past-incident runbooks are onboarding material, not the primary way to debug.
