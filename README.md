# Vet

Monorepo with a Next.js frontend (`apps/web`) and a Strapi CMS (`apps/cms`), backed by PostgreSQL. Everything runs in Docker.

## Stack

| App | Tech | Local port |
|---|---|---|
| web | Next.js 15 | 3000 |
| cms | Strapi 5 | 1337 |
| db | PostgreSQL 16 | 5432 |

---

## First-time setup

### 1. Copy env files

```bash
cp apps/cms/.env.example apps/cms/.env
cp apps/web/.env.example apps/web/.env
```

### 2. Fill in Strapi secrets (`apps/cms/.env`)

Generate each value with:

```bash
openssl rand -base64 32
```

You need **4 keys** for `APP_KEYS` (comma-separated) and **one each** for the rest:

```env
APP_KEYS=<key1>,<key2>,<key3>,<key4>
API_TOKEN_SALT=<generated>
ADMIN_JWT_SECRET=<generated>
TRANSFER_TOKEN_SALT=<generated>
JWT_SECRET=<generated>
```

Keep `DATABASE_HOST=postgres` — that's the Docker service name, not localhost.

### 3. Set the Strapi API token (`apps/web/.env`)

Leave `STRAPI_API_TOKEN` blank for now. After the stack is running:

1. Open `http://localhost:1337/admin` and create your admin account
2. Go to **Settings → API Tokens → Create new API Token**
3. Set type to **Full access** (or scope it down as needed)
4. Copy the token and paste it into `apps/web/.env`:

```env
STRAPI_API_TOKEN=<token from Strapi admin>
```

Then restart the web container:

```bash
docker compose restart web
```

---

## Running the project

```bash
# Start all services (dev mode with hot reload)
docker compose up --build

# Detached
docker compose up --build -d

# Logs
docker compose logs -f web
docker compose logs -f cms

# Stop
docker compose down

# Stop and wipe the database volume
docker compose down -v
```

## Production

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up --build
```

---

## Project structure

```
apps/
  web/          Next.js frontend
    app/        App Router pages (/, /about, /contact)
    lib/        Strapi API client
  cms/          Strapi CMS
    src/api/    Content types (add via Strapi admin or CLI)
    config/     Database and server config
docker-compose.yml       Dev (hot reload)
docker-compose.prod.yml  Prod overrides (standalone builds)
```
