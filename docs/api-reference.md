# API reference (pointers)

Opoha does not yet ship a generated OpenAPI/GraphQL HTML explorer on this docs site. Use these **canonical sources** until codegen docs are published.

## GraphQL (runtime)

| Source | What it covers |
|--------|----------------|
| Running core | `POST/GET http://localhost:4000/graphql` (Apollo playground in development) |
| `opoha-core` README | Module GraphQL surfaces, auth, walking skeleton |
| Workspace GraphQL deprecation policy | `docs/readiness/graphql-deprecation-policy.md` — deprecation window before removal after `1.0.0` |
| Public API freeze | `docs/readiness/public-api-freeze-plan.md`, `docs/readiness/v1-api-freeze-plan.md` |

Clients should send `X-API-Version: 1` where documented by core.

## Typed client (`@opoha/sdk`)

| Source | What it covers |
|--------|----------------|
| `@opoha/sdk` README | `createOpohaClient`, login, catalog, cart, checkout, orders, payments |
| Generated operations | Package GraphQL documents / codegen output inside `opoha-sdk` |

Storefronts and Admin talk to core **only** through GraphQL (never direct TypeORM).

## Plugin contracts (`@opoha/plugin-sdk`)

| Source | What it covers |
|--------|----------------|
| `@opoha/plugin-sdk` README | `definePlugin`, manifests, frozen exports |
| [Plugin author guide](./plugin-author-guide.md) | Authoring workflow |
| Stable events / PluginContext | Workspace `docs/readiness/stable-events-and-plugin-context.md` |
| Public API inventory | Workspace `docs/readiness/v1-public-api-inventory.md` |

## CLI

| Command | Docs |
|---------|------|
| `opoha doctor` | [Deployment](./deployment.md) |
| `opoha generate plugin` | [Plugin template](./plugin-template.md) |
| `opoha generate storefront` | [Storefront template](./storefront-template.md) |
| `create-opoha` | [Getting started](./getting-started.md) |

## Related journeys

- [Getting started](./getting-started.md)  
- [Deployment](./deployment.md)  
- [Plugin author guide](./plugin-author-guide.md)  
- [Storefront template](./storefront-template.md)  
