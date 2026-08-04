# Getting started (install)

Install a local Opoha commerce app: scaffold → infrastructure → migrate → seed → boot GraphQL.

**Persistence:** TypeORM only (ADR-0010). Do not introduce Prisma for application data.

## Prerequisites

- Node.js **≥ 20**
- [pnpm](https://pnpm.io/) **11.x**
- Docker (Postgres 16 + Redis 7 via the default template compose file)

## Scaffold

### Full-stack app (recommended)

From a sibling checkout of the Opoha packages (local multi-repo):

```bash
pnpm exec create-opoha my-store --link
cd my-store
```

Published packages:

```bash
npx @opoha/create-opoha my-store
# or: pnpm dlx @opoha/create-opoha my-store
cd my-store
```

### Storefront-only (Next.js)

If you already have a running Opoha GraphQL API and only need a storefront:

```bash
pnpm exec create-opoha my-shop --template storefront --link
# or: npx @opoha/create-opoha my-shop --template storefront
# or: opoha generate storefront my-shop
```

See [storefront-template.md](./storefront-template.md).

## Boot the API

```bash
pnpm install
cp .env.example .env
docker compose up -d
pnpm migrate
pnpm seed
pnpm dev
```

| Surface | Default |
|---------|---------|
| GraphQL | `http://localhost:4000/graphql` |
| Admin (when wired) | `http://localhost:3001` |

## Verify

```bash
pnpm exec opoha doctor
```

Doctor checks Node version, env presence (`DATABASE_URL`, `REDIS_URL`, `JWT_SECRET`), TCP reachability for Postgres/Redis, and lockfile plugin contract compatibility. Secret **values are never printed**.

For production hardening expectations, see [deployment.md](./deployment.md).

## Next steps

1. [Deployment](./deployment.md) — production env + doctor checklist  
2. [Plugin author guide](./plugin-author-guide.md) — extend with plugins  
3. [Storefront template](./storefront-template.md) — Next.js against GraphQL  
4. [API reference](./api-reference.md) — SDK + GraphQL pointers  
5. [Upgrade from v0.9](./upgrade-from-v0.9.md) — migrate an existing app to 1.0  

## Related

- `@opoha/create-opoha` package README  
- `opoha-core` walking skeleton (`pnpm walking-skeleton`) for automated install→order smoke  
