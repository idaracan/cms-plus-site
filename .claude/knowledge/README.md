# Knowledge Index — Retrieval Strategy

Path-specific rules in `.claude/rules/` auto-inject the relevant knowledge files when you open a matching path. You rarely need to load these manually.

| File | What's inside | When to read |
|---|---|---|
| `architecture.md` | System design, component layout, data flow, ports | Any cross-layer or infrastructure change |
| `decisions.md` | Locked architectural decisions with rationale | Before proposing something that might conflict with prior choices |
| `patterns.md` | Established ways of doing things in this project | Every new code path |
| `gotchas.md` | Cross-cutting tripwires (incident or debug-driven) | Always — load eagerly |
| `contribution-rules.md` | Hard rules for writing new code | Any new feature or refactor |
| `anti-patterns.md` | Explicit no-go list — stop and flag | Before implementing a pattern that might be disallowed |
| `open-questions.md` | Live `[BLOCKER]` / `[OPEN]` items | Scoping, estimating, before committing to an approach |
| `domains/web.md` | Next.js frontend specifics | When working in `apps/web/` |
| `domains/cms.md` | Strapi CMS specifics | When working in `apps/cms/` |
| `domains/infra.md` | Docker and CI specifics | When working on compose, Dockerfiles, or workflows |
