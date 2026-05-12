# Contribution Rules

Hard rules for writing new code in this project.

1. **Never ship without `/verify`.** TypeScript must compile and lint must pass before marking a task done.
2. **Server components by default.** Add `"use client"` only when the component requires interactivity or browser APIs.
3. **No `useEffect` for data fetching.** Use server components and `lib/strapi.ts` instead.
4. **`STRAPI_API_TOKEN` is server-only.** Never expose it to client-side code or prefix it with `NEXT_PUBLIC_`.
5. **Strapi config files are CommonJS JS, not TypeScript.** Do not convert them or introduce `.ts` config files.
6. **Validate input at system boundaries.** The contact form server action must validate all fields before calling Strapi.
7. **No `any` in TypeScript** without a comment justifying why it cannot be typed.
8. **Secrets in env files only.** Never hardcode tokens, passwords, or keys — not even in dev config.
9. **Use `cn()` from `lib/utils.ts`** for all conditional Tailwind class merging — never string concatenation.
10. **Use `/remember`** for persistent learnings — not inline code comments.
11. **Extend existing shadcn/ui components** before creating new ones. Check `components/layout/sections/` first.
12. **After any `package.json` change**, follow the Docker rebuild pattern (drop volume, rebuild) — not just restart.
