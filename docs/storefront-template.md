# Official Opoha storefront starter (v1.0)

Minimal **Next.js App Router** storefront that talks to Opoha core GraphQL via `@opoha/sdk`.
No TypeORM in the storefront — persistence stays in core (ADR-0010).

This is the **documented v1.0 storefront path** (PRD: Next.js minimum). Vue / Remix / Astro starters are Should / later.

## Generate

```bash
opoha generate storefront my-shop
# or
create-opoha my-shop --template storefront
# local multi-repo:
create-opoha my-shop --template storefront --link
```

**CLI source of truth:** `@opoha/cli` → `templates/storefront`  
**create-opoha mirror:** `create-opoha/templates/storefront`  
**Inventory constant:** `OFFICIAL_STOREFRONT_TEMPLATE_FILES`

## Layout

| Path | Role |
|------|------|
| `src/app/page.tsx` | Home — brand + `createOpohaClient().ping()` probe |
| `src/app/layout.tsx` | Root layout |
| `.env.example` | `NEXT_PUBLIC_OPOHA_GRAPHQL_URL` |
| `next.config.mjs` / `tsconfig.json` | Next.js + TypeScript |
| `pnpm-workspace.yaml` | `allowBuilds: sharp` — Next.js image optimization needs sharp's install script |

Storefront pages render per-request (`export const dynamic = 'force-dynamic'`),
so `pnpm build` never depends on a live `opoha-core` connection.

## Develop

```bash
cp .env.example .env.local
# Point at a running core GraphQL (default create-opoha API):
# NEXT_PUBLIC_OPOHA_GRAPHQL_URL=http://localhost:4000/graphql
pnpm install
pnpm dev
```

Prerequisite: a running Opoha API — see [getting-started.md](./getting-started.md).

## Client usage

Use `@opoha/sdk` for typed GraphQL — see [api-reference.md](./api-reference.md) and the SDK README (catalog, cart, checkout, orders).

## Related

- [Getting started](./getting-started.md)  
- [Plugin template](./plugin-template.md)  
