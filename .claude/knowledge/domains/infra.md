# Domain: Infrastructure

## Docker Compose

| File | Purpose |
|---|---|
| `docker-compose.yml` | Dev stack — bind mounts, hot reload, `target: dev` |
| `docker-compose.prod.yml` | Prod overrides — `target: prod`, no bind mounts |

## Compose commands

```bash
# Dev
docker compose up --build         # build and start all services
docker compose up --build -d      # detached
docker compose logs <service> -f  # follow logs
docker compose restart <service>  # restart without rebuild
docker compose down               # stop (safe — volumes preserved)
docker compose down -v            # DANGER: wipes all volumes including pg_data

# Prod
docker compose -f docker-compose.yml -f docker-compose.prod.yml up --build
```

## Rebuild a single service after package.json change

```bash
docker compose rm -f <service>
docker volume rm vet_<service>_node_modules
docker compose up --build -d <service>
```

## GitHub Actions

Workflow at `.github/workflows/ci.yml`. Runs TypeScript check and build for `apps/web`, TypeScript check for `apps/cms`. Actions pinned to commit SHAs, `permissions: contents: read`.

## SSH / Git

Personal GitHub account (`idaracan`) uses SSH alias `github-personal` configured in `~/.ssh/config`. Remote URL: `git@github-personal:idaracan/cms-plus-site.git`. Work credentials are on HTTPS — the SSH alias isolates them.
