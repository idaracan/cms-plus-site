# Domain: Next.js Frontend (apps/web)

## Template

Based on `nobruf/shadcn-landing-page` — Next.js 14, shadcn/ui, Tailwind CSS 3, dark mode via `next-themes`.

## Key files

| File | Purpose |
|---|---|
| `app/page.tsx` | Landing page — imports all section components |
| `app/about/page.tsx` | About page — fetches content from Strapi |
| `app/contact/page.tsx` | Contact page — server action posts to Strapi |
| `lib/strapi.ts` | Strapi API client — all fetch calls go here |
| `components/layout/sections/` | Landing page sections (hero, features, contact, etc.) |
| `components/ui/` | Generated shadcn/ui primitives — do not edit directly |
| `next.config.mjs` | Next.js config — `output: "standalone"` required for Docker prod |

## Strapi content types expected

- `About` (single type) — `title`, `content` fields
- `Contact Submission` (collection type) — `name`, `email`, `message`

## Environment variables

| Var | Side | Purpose |
|---|---|---|
| `NEXT_PUBLIC_STRAPI_URL` | Client | Public Strapi URL for browser-visible references |
| `STRAPI_URL` | Server | Strapi URL for server-side fetches (inside Docker: `http://cms:1337`) |
| `STRAPI_API_TOKEN` | Server | Strapi API token — never expose client-side |
