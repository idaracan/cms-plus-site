---
paths:
  - "docker-compose*.yml"
  - "apps/*/Dockerfile"
  - ".github/**/*"
---

# Infrastructure Rules

@../knowledge/gotchas.md
@../knowledge/domains/infra.md

When working on Docker or CI:
- `docker compose down` is safe. `docker compose down -v` WIPES THE DATABASE — always confirm with the user first.
- Named volumes (`pg_data`, `cms_node_modules`, `web_node_modules`, `web_next`) must be dropped explicitly when dependencies change.
- GitHub Actions: pin third-party actions to full commit SHA, set `permissions: contents: read`, never interpolate event inputs directly in `run:` blocks.
- Dev compose uses bind mounts for hot reload; prod compose (`docker-compose.prod.yml`) uses `target: prod` with no bind mounts.
