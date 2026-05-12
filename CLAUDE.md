# vet — cms-plus-site

> Claude Code-native scaffold. Other agents reading `AGENTS.md` (symlink): the "Orchestration" and `.claude/*` references below assume Claude Code's subagent/rule loader — skip those sections; portable content is Source of truth, Commands, and Quick links.

## At a glance

| | |
|---|---|
| **What** | Vet clinic website — landing page, about, contact form; shop planned |
| **Stack** | Next.js 14 + Strapi 5 + PostgreSQL 16 + Docker |
| **Repo** | `git@github-personal:idaracan/cms-plus-site.git` |
| **Phase** | Initial scaffold — content wiring to Strapi next |

## Source of truth

- `.claude/knowledge/architecture.md` — system design, services, volumes
- `.claude/knowledge/decisions.md` — locked decisions + rationale
- `.claude/knowledge/domains/web.md` — Next.js frontend specifics
- `.claude/knowledge/domains/cms.md` — Strapi CMS specifics
- `.claude/knowledge/domains/infra.md` — Docker and CI specifics

## Orchestration

Top-level Claude is the **orchestrator**, not the implementer. Delegate via the `Agent` tool. Agents do not call each other — the graph is flat.

| Task surface | Primary agent | Notes |
|---|---|---|
| Next.js pages, components, Strapi wiring | `next-dev` | Server components by default |
| Strapi content types, config, admin | `cms-dev` | JS config only, not TS |
| Docker, compose, CI/CD | `infra-dev` | Confirm before `down -v` |
| New UI sections, shadcn/ui components | `component-author` | Extend template sections first |
| Code review before merge | `reviewer` | BLOCKER / MAJOR / MINOR format |
| Cross-layer or new service proposals | `architect` | Analysis only, no implementation |

### Rules of engagement

- **Never implement feature code** when a specialist agent exists for that surface.
- Launch agents in parallel when work is independent.
- After any non-trivial task, run `/remember` to capture learnings.
- When `reviewer` returns BLOCKER items, fix before marking complete.

## Commands

```bash
# Dev
docker compose up --build -d
docker compose logs web -f
docker compose logs cms -f
docker compose down

# After package.json change in either app
docker compose rm -f <service> && docker volume rm vet_<service>_node_modules && docker compose up --build -d <service>

# Prod
docker compose -f docker-compose.yml -f docker-compose.prod.yml up --build
```

## Contribution rules (hard)

- **Never ship without `/verify`.** TypeScript must compile and lint must pass.
- **Server components by default.** `"use client"` only for interactivity or browser APIs.
- **`STRAPI_API_TOKEN` is server-only.** Never in client-side code or `NEXT_PUBLIC_*` vars.
- **Strapi config is CommonJS JS, not TypeScript.** Do not add `.ts` files under `apps/cms/config/`.
- **Secrets in env files only.** Never hardcode — not even in dev config.
- **Follow the Docker rebuild pattern** after any `package.json` change (drop volume, rebuild).

Full list: `.claude/knowledge/contribution-rules.md`

## Anti-patterns (hard no)

- Hardcoded secrets anywhere in the codebase
- `STRAPI_API_TOKEN` in client-side code or `NEXT_PUBLIC_*`
- TypeScript config files in `apps/cms/config/`
- `docker compose down -v` without explicit user confirmation
- Calling Strapi API directly from components — use `lib/strapi.ts`
- Removing `output: "standalone"` from `next.config.mjs`
- Committing `.env` files

Full list: `.claude/knowledge/anti-patterns.md`

## Knowledge index

| File | What's inside | When to read |
|---|---|---|
| `.claude/knowledge/README.md` | File index + retrieval strategy | First session in this repo |
| `.claude/knowledge/architecture.md` | Services, volumes, data flow | Any cross-layer change |
| `.claude/knowledge/decisions.md` | Locked decisions + rationale | Before proposing something new |
| `.claude/knowledge/patterns.md` | Established conventions | Every new code path |
| `.claude/knowledge/gotchas.md` | Tripwires from debugging | Always — load eagerly |
| `.claude/knowledge/contribution-rules.md` | Hard coding rules | Any new feature or refactor |
| `.claude/knowledge/anti-patterns.md` | Explicit no-go list | Before implementing a pattern |
| `.claude/knowledge/open-questions.md` | Live blockers | Scoping or estimating work |
| `.claude/knowledge/domains/web.md` | Next.js frontend details | When working in `apps/web/` |
| `.claude/knowledge/domains/cms.md` | Strapi CMS details | When working in `apps/cms/` |
| `.claude/knowledge/domains/infra.md` | Docker and CI details | When working on infra |

## Open questions

See `.claude/knowledge/open-questions.md`. Items tagged `[BLOCKER]` gate scope.

**Directive**: when a task touches a surface governed by an open `[BLOCKER]`, surface it at the top of your response. Don't silently pick an interpretation — flag it, propose the scaffold default, and note what changes if resolved differently.

## Project-local skills

| Skill | Purpose |
|---|---|
| `/verify` | TypeScript compile + lint + container health check |
| `/remember` | Capture learnings into `.claude/knowledge/` |
