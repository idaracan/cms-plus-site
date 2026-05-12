# Open Questions

### [OPEN] Q1.1 — Strapi API token rotation strategy

**Touches**: `apps/web`, `apps/cms`, deployment
**Owner**: Ivan
**Default if unresolved**: Single long-lived full-access token stored in `apps/web/.env`
**Impact if answer goes the other way**: Scoped read-only token per content type would reduce blast radius if the web env is compromised

### [OPEN] Q1.2 — Production hosting target

**Touches**: `docker-compose.prod.yml`, CI/CD pipeline, `apps/cms/config/database.js`
**Owner**: Ivan
**Default if unresolved**: Self-hosted VPS with Docker Compose prod stack
**Impact if answer goes the other way**: Managed platforms (Railway, Render, Fly.io) would change the Dockerfile and env strategy

### [OPEN] Q1.3 — Shop timeline and Medusa.js integration

**Touches**: `apps/`, `docker-compose.yml`, `architecture.md`
**Owner**: Ivan
**Default if unresolved**: Shop deferred — no Medusa service added yet
**Impact if answer goes the other way**: Medusa as `apps/shop` adds a third Docker service and a second database or shared Postgres schema
