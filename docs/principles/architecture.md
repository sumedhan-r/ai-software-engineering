# Architecture

Agent: read this before adding a module, calling an external system (DB, queue, third-party API), adding configuration, or changing how the service starts, stops, or is deployed. Product-specific infrastructure choices are in [decisions/](../decisions/); how to run things locally is in [guides/infra.md](../guides/infra.md).

---

<!-- Scaffold only. Sumedhan writes the rules.
     Format per rule: **ARC-n — <one-line rule>.** then Rule / Why / In code.
     Aim for 6-8 rules, ~300-600 words. A rule belongs here only if it holds for
     every product and an agent can see it in a diff. Product-specific choices
     (which DB, helm vs compose) go in decisions/.

     Candidate topics (pick, merge or drop):

     How code meets infrastructure
     - Config comes only from env vars; nothing hardcoded per environment (Twelve-Factor).
     - Every external system sits behind an interface in interfaces/, implemented in connectors/
       (Clean Architecture dependency rule: domain and services never import frameworks, DB or HTTP clients).
     - Services keep no local state; anything that must survive a restart lives in a backing service.

     How it behaves when running
     - Every network call has a timeout and a bounded retry; only idempotent operations are retried.
     - Health/readiness checks exposed; graceful shutdown on SIGTERM.
     - Dev and prod run the same container image; only config changes.
     - Schema changes go through migrations and stay backward-compatible with the previous release.

     Overlaps observability (health checks, timeouts): cross-link OBS-n rules instead of repeating them.
     Layer import rules (which layer may import which) go in guides/service-layer.md.

     Sources: Clean Architecture (Martin), dependency rule only; The Twelve-Factor App (12factor.net);
     Fundamentals of Software Architecture (Richards & Ford); Designing Data-Intensive Applications (Kleppmann).
-->

## Rules

<!-- ARC-1 ... -->

---

## Don't

<!-- - Do not ... -->
