---
paths:
  - "apps/cms/**/*"
---

# Strapi CMS Rules

@../knowledge/gotchas.md
@../knowledge/domains/cms.md

When working in `apps/cms/`:
- Config files (`config/*.js`) are plain CommonJS — not TypeScript. TypeScript configs caused esbuild-register load failures.
- After changing `package.json`, drop the `vet_cms_node_modules` volume before rebuilding — plain restart reuses the stale volume.
- `zod@^4.0.0` must stay in dependencies — required for the Vite admin UI build (`zod/v4` subpath).
- `DATABASE_HOST` must be `postgres` (Docker service name) inside the container, not `localhost`.
- `apps/cms/public/uploads/` is bind-mounted — the directory must exist on the host or Strapi will fail to start.
