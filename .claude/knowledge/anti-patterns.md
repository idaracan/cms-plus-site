# Anti-patterns

If a task asks you to do any of these, stop, flag it to the user, and propose the correct alternative.

1. **Hardcoded secrets** — even in dev config or example files. Use env vars and `.env.example` placeholders.
2. **`STRAPI_API_TOKEN` in client-side code** — it must stay server-only. Flag immediately if it appears in a `"use client"` file or `NEXT_PUBLIC_*` var.
3. **TypeScript config files in `apps/cms/config/`** — Strapi's esbuild-register cannot reliably load them. Keep all CMS config as `.js` CommonJS.
4. **`docker compose down -v` in scripts or instructions** — this wipes the database. Always require explicit user confirmation.
5. **Calling the Strapi API directly from a component** — all Strapi fetches go through `apps/web/lib/strapi.ts`.
6. **`useEffect` for data fetching** — use server components instead.
7. **`npm install -g` or global package installs** — everything runs in Docker; global installs on the host are irrelevant.
8. **Removing `output: "standalone"` from `next.config.mjs`** — breaks the production Docker image.
9. **Committing `.env` files** — only `.env.example` belongs in git.
10. **Force push to `main`** — always branch and PR.
11. **Interpolating GitHub event inputs directly in `run:` blocks** — pass through `env:` vars instead.
12. **Installing a new UI library alongside shadcn/ui** — extend the existing system; don't introduce a second component library.
