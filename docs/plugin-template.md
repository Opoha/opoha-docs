# Official Opoha plugin template (v0.7)

Canonical scaffold used by `opoha generate plugin`. Matches ADR-0003 / `@opoha/plugin-sdk`
contract shape. Runtime reference: `@opoha/plugin-sample` (loader + registry smoke).

**Source of truth:** `@opoha/cli` → `templates/plugin`  
**Inventory constant:** `OFFICIAL_PLUGIN_TEMPLATE_FILES`

## Generate

```bash
opoha generate plugin my-widget
opoha generate plugin my-widget --link   # file: @opoha/plugin-sdk (monorepo)
```

## Required layout

| Path | Role |
|------|------|
| `opoha.plugin.json` | Manifest |
| `package.json` | Package + `opoha` block |
| `src/index.ts` | `definePlugin` lifecycle stubs |
| `src/index.test.ts` | Smoke test |
| `tsconfig.json` / `tsconfig.build.json` | Typecheck + emit |
| `vitest.config.ts` | Unit tests |
| `pnpm-workspace.yaml` | Local `file:` SDK link |
| `.gitignore` / `README.md` | DX |

Generated plugins are **standalone** (no monorepo `@opoha/typescript-config` / `@opoha/vitest-config`
file deps) so authors can build outside the Opoha sibling workspace.

## Rules

- Contract version must match `@opoha/plugin-sdk` (`0.1` for v0.7)
- Do not import `@opoha/core` from plugins
- Plugin-owned TypeORM only (ADR-0010 / ADR-0005) — never mutate core tables
- Register GraphQL / admin / listeners via `PluginContext` in `boot`

See also: [storefront-template.md](./storefront-template.md).
