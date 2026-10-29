# ai-software-engineering

This repository contains a cohesive arrangement of files that are necessary for a well maintained and deployable software product. All experience gathered here can be used as a kick start for any new software initiative using AI as developer

## Layout

```
AGENTS.md            # entry point for AI agents: stack, commands, rules, doc index
CLAUDE.md            # imports AGENTS.md
docs/
  INDEX.md           # map of every doc and when to read it
  glossary.md        # domain and project terms
  principles/        # conceptual: design philosophy, observability, refactoring
  guides/            # instructional: API, schemas, repository, service layer, testing, infra
  decisions/         # why X was chosen over Y, one file per decision
  specs/             # feature specs and technical specs
ideas/               # product ideas to test and validate
reference/           # one small, complete "golden path" feature
  src/
  tests/
infra/
  compose/           # local deployment with Docker Compose
  helm/              # Kubernetes deployment (later)
scripts/             # helper scripts
.claude/commands/    # reusable prompts as slash commands
.github/workflows/   # CI
```

## How content gets written

- Principles, ADRs, spec content, and stack choices are written by hand.
- Guides and the reference feature are drafted by hand, then reviewed with AI for gaps and length.
- Templates, folders, CI, and scripts are scaffolding and can be generated.
