---
name: verify
description: Build + lint check for both apps without running the full Docker stack
---

# Verify

Run this after any non-trivial change before committing.

## Steps

1. Check web TypeScript compiles cleanly:
   ```bash
   docker compose exec web npx tsc --noEmit
   ```

2. Check web linter:
   ```bash
   docker compose exec web npm run lint
   ```

3. Confirm both containers are healthy:
   ```bash
   docker compose ps
   docker compose logs web --tail=10
   docker compose logs cms --tail=10
   ```

4. For production build validation (before deploy):
   ```bash
   docker compose -f docker-compose.yml -f docker-compose.prod.yml build
   ```

## Rules

- Never mark a task complete if tsc or lint fails
- A container in restart loop is a blocker — check logs before proceeding
