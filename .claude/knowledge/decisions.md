# Locked Decisions

1. **Monorepo over polyrepo** — Frontend and CMS share a lifecycle; content model changes and the frontend code that consumes them land in the same PR. Revisit only if teams split ownership of the apps.

2. **Docker-first development** — No local Node/npm required to run the project. All dev, build, and run workflows go through `docker compose`. Revisit only if Docker overhead becomes prohibitive.

3. **Strapi config in plain JavaScript (CommonJS)** — TypeScript config files caused esbuild-register load failures at runtime. Strapi 5 loads config via `require()` and the TS compilation was unreliable. Revisit if Strapi fixes its TS config loading in a future version.

4. **PostgreSQL over SQLite** — SQLite cannot survive container restarts reliably. Postgres is the production-grade choice and runs in Docker locally. Do not switch back.

5. **Next.js over plain React** — SSR/ISR required for SEO on landing and about pages. Server actions handle the contact form without a separate API route.

6. **shadcn/ui + Tailwind CSS** — Chosen via the `nobruf/shadcn-landing-page` open-source template. All new components should extend this system rather than introducing a second UI library.

7. **npm over pnpm** — User does not have pnpm installed locally. All workspace and Docker scripts use npm.
