# Architecture

## Overview

Monorepo with two apps and a shared PostgreSQL database, all containerized.

```
vet/
├── apps/web/     Next.js 14 frontend (shadcn/ui + Tailwind)
├── apps/cms/     Strapi 5 CMS (content API + admin)
└── docker-compose.yml  dev stack
```

## Services

| Service | Image / Build | Port | Role |
|---|---|---|---|
| `web` | `apps/web` Dockerfile | 3000 | Next.js frontend |
| `cms` | `apps/cms` Dockerfile | 1337 | Strapi CMS + admin |
| `postgres` | postgres:16-alpine | 5432 | Shared database |

## Data Flow

```
Browser → Next.js (SSR/ISR) → Strapi REST API → PostgreSQL
                ↑
         Strapi Admin UI (1337/admin)
```

## Volume Strategy

| Volume | Type | Contents |
|---|---|---|
| `pg_data` | Named | PostgreSQL data — persists across restarts |
| `cms_node_modules` | Named | Strapi node_modules — must drop when package.json changes |
| `web_node_modules` | Named | Next.js node_modules — must drop when package.json changes |
| `web_next` | Named | Next.js `.next` build cache |
| `apps/cms/public/uploads/` | Bind | Strapi uploaded files — persisted on host |
| `apps/web/` | Bind | Next.js source — hot reload in dev |
| `apps/cms/src/` | Bind | Strapi source — hot reload in dev |
| `apps/cms/config/` | Bind | Strapi config — picked up on restart |

## Planned additions

- **Shop**: Medusa.js as `apps/shop` — future, third Docker service
