# Domain: Strapi CMS (apps/cms)

## Version

Strapi 5.45.1, Community Edition, PostgreSQL dialect.

## Key files

| File | Purpose |
|---|---|
| `config/database.js` | PostgreSQL connection config |
| `config/server.js` | Host, port, app keys |
| `config/admin.js` | Admin JWT secret, API token salt, transfer token salt |
| `src/index.js` | Strapi entry point (register/bootstrap hooks) |
| `src/api/` | Content type definitions (generated via Strapi admin or CLI) |
| `public/uploads/` | Uploaded media — bind-mounted to host |

## Content types to create (via Strapi admin)

- **About** (Single Type): `title` (Text), `content` (Rich Text)
- **Contact Submission** (Collection Type): `name` (Text), `email` (Email), `message` (Long Text)

## Environment variables

| Var | Purpose |
|---|---|
| `APP_KEYS` | 4 comma-separated base64 keys |
| `API_TOKEN_SALT` | Salt for API token generation |
| `ADMIN_JWT_SECRET` | Admin panel JWT secret |
| `TRANSFER_TOKEN_SALT` | Data transfer token salt |
| `JWT_SECRET` | Users-permissions JWT secret |
| `DATABASE_HOST` | `postgres` inside Docker, `localhost` externally |
| `DATABASE_PORT` | `5432` |
| `DATABASE_NAME` | `strapi` |
| `DATABASE_USERNAME` | `strapi` |
| `DATABASE_PASSWORD` | `strapi` |

## Known quirks

- `zod@^4.0.0` must be in `dependencies` — resolves `zod/v4` subpath for Vite admin UI build
- Config files must be `.js` CommonJS — TypeScript configs fail at runtime
- `styled-components@^6.0.0` is auto-installed by Strapi on first start — expected behavior
