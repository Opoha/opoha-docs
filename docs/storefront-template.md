# Official Opoha storefront starter (v0.7)

Minimal **Next.js App Router** storefront that talks to Opoha core GraphQL via `@opoha/sdk`.
No TypeORM in the storefront — persistence stays in core (ADR-0010).

## Generate

```bash
opoha generate storefront my-shop
# or
create-opoha my-shop --template storefront
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

## Develop

```bash
cp .env.example .env.local
pnpm install
pnpm dev
```

Point the GraphQL URL at a running Opoha core server.

See also: [plugin-template.md](./plugin-template.md).
