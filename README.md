# Opoha Docs

Official technical documentation for Opoha (v1.0 DX journeys).

## Purpose

Publish getting started, deployment, plugin development, API reference pointers, and storefront guides for store, plugin, and enterprise developers.

## Boundaries

- Documentation only — not the marketing website (`opoha-website`)
- Does not ship commerce runtime or plugins
- Content authority for product docs; architecture source of truth remains `opoha-workspace` until published here

## Journeys (v1.0)

| Journey | Doc |
|---------|-----|
| Install | [docs/getting-started.md](./docs/getting-started.md) |
| Deploy | [docs/deployment.md](./docs/deployment.md) |
| Upgrade (v0.9 → v1.0) | [docs/upgrade-from-v0.9.md](./docs/upgrade-from-v0.9.md) |
| Plugin author | [docs/plugin-author-guide.md](./docs/plugin-author-guide.md) |
| Storefront (Next.js) | [docs/storefront-template.md](./docs/storefront-template.md) |
| API reference pointers | [docs/api-reference.md](./docs/api-reference.md) |

## Templates & extras

- [Plugin template](./docs/plugin-template.md) — `opoha generate plugin`
- [Plugin CI template](./docs/plugin-ci-template.md) — GitHub Actions for authors
- [Storefront template](./docs/storefront-template.md) — Next.js App Router + `@opoha/sdk`
- [Marketplace flow](./docs/marketplace-flow.md) — Phase 6
- [Analytics storefront hooks](./docs/analytics-storefront-hooks.md) — Phase 4

## Status

Markdown docs site for Phase 9 DX. Full static-site tooling may follow; journey coverage is the v1.0 gate.
