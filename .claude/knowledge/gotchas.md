# Gotchas

Keep under 50 lines. Overflow to domain files.

[DOCKER:cms-node-modules] The `vet_cms_node_modules` named volume must be dropped explicitly when `apps/cms/package.json` changes — a plain `docker compose restart` or `--build` reuses the stale volume and the new package is never installed.

[DOCKER:volume-wipe] `docker compose down -v` deletes ALL named volumes including `pg_data`, destroying the database. Plain `docker compose down` (no `-v`) is safe.

[STRAPI:zod-v4] `zod@^4.0.0` must remain in `apps/cms/package.json`. Strapi 5's Vite admin build references the `zod/v4` subpath which only exists in zod v4+. Removing it causes the admin UI to fail to load.

[STRAPI:ts-config] Strapi 5 config files must be plain CommonJS JavaScript (`.js`), not TypeScript. The esbuild-register runtime loader failed to process TypeScript config files reliably, causing `db.config.connection` to be undefined.

[STRAPI:database-host] Inside Docker, `DATABASE_HOST` must be `postgres` (the compose service name). Using `localhost` causes connection refused because the CMS container cannot reach its own loopback for the postgres service.

[STRAPI:uploads-dir] `apps/cms/public/uploads/` must exist on the host before starting the CMS container. The directory is bind-mounted and Strapi's upload provider checks for it at startup.

[GIT:submodule-trap] Copying a cloned repo into a subdirectory without removing its `.git` folder causes git to register it as a submodule. Remove `.git` from the copied directory and run `git rm --cached <dir> && git add <dir>` to re-add as regular files.

[NEXT:standalone] `output: "standalone"` in `apps/web/next.config.mjs` is required for the production Docker image. Removing it breaks the prod build — the `node server.js` entrypoint won't exist.
