---
paths:
  - "apps/web/**/*"
---

# Next.js Frontend Rules

@../knowledge/patterns.md
@../knowledge/gotchas.md
@../knowledge/domains/web.md

When working in `apps/web/`:
- Default to server components. Add `"use client"` only for interactivity or browser APIs.
- Fetch Strapi content via `apps/web/lib/strapi.ts` — never call the Strapi API directly from components.
- `STRAPI_API_TOKEN` is server-only — never expose it to client-side code or `NEXT_PUBLIC_*`.
- `output: "standalone"` in `next.config.mjs` is required for the Docker prod image — do not remove it.
- The template uses shadcn/ui — extend existing components in `components/layout/sections/` before creating new ones.
