# Patterns

Established conventions for this project. Populated via `/remember`.

## Strapi API fetch pattern

Server-side Strapi calls go through `apps/web/lib/strapi.ts`. Use `fetchStrapi<T>(path)` — it handles auth headers and `revalidate`.

```ts
export function getAbout() {
  return fetchStrapi<AboutData>("/about?populate=*");
}
```

Add a typed getter per content type. Never call `fetch()` directly against Strapi from a page or component.

## Contact form pattern

Use Next.js Server Actions for the contact form — no separate API route needed. The server action calls the Strapi REST API with `STRAPI_API_TOKEN` (server-only env var).

## Docker rebuild pattern

When `package.json` changes in either app:
1. Stop and remove the container: `docker compose rm -f <service>`
2. Drop the node_modules volume: `docker volume rm vet_<service>_node_modules`
3. Rebuild: `docker compose up --build -d <service>`

Skipping step 2 leaves stale packages in the volume.
