# Plugin author guide

Build Opoha plugins against `@opoha/plugin-sdk` only. Plugins must **not** import `@opoha/core` or mutate core tables. Plugin-owned TypeORM entities are allowed when declared by the plugin (ADR-0005 / ADR-0010).

## Scaffold

```bash
opoha generate plugin my-widget
opoha generate plugin my-widget --link   # file: @opoha/plugin-sdk (monorepo)
```

Generated layout matches the [official plugin template](./plugin-template.md). Runtime reference: `@opoha/plugin-sample`.

## Contract

| Item | v1.0 expectation |
|------|------------------|
| Package | `@opoha/plugin-sdk` |
| `PLUGIN_CONTRACT_VERSION` | `0.1` (frozen through package `1.0.0` — see workspace freeze docs) |
| Manifest | `opoha.plugin.json` or `package.json#opoha` with matching `contractVersion` |

```ts
import { definePlugin } from '@opoha/plugin-sdk';

export default definePlugin({
  id: 'my-widget',
  boot(ctx) {
    ctx.registerPaymentProvider({
      code: 'my-widget',
      displayName: 'My Widget',
    });
    // ctx.registerGraphQL / registerAdmin / registerShippingMethod / …
  },
});
```

## Registration surfaces

Use `PluginContext` in `boot` (and other lifecycles as documented in the SDK):

- Engine providers: payment, shipping, tax, storage  
- GraphQL extensions  
- Admin navigation / pages  
- Event listeners  
- Scheduled jobs / workflow actions / rule actions (when applicable)

Stable events and PluginContext inventory: workspace `docs/readiness/stable-events-and-plugin-context.md` and `docs/readiness/v1-public-api-inventory.md`.

## Develop locally

```bash
pnpm install
pnpm build
pnpm test
pnpm typecheck
```

Install into an app (updates `opoha.config.json`):

```bash
opoha plugin install .
# or add a path / package name to opoha.config.json "plugins"
```

See [Using plugins](./using-plugins.md).

## CI template

Generated plugins include `.github/workflows/ci.yml` (install → typecheck → test → build). Copy or keep that workflow when publishing third-party plugins. See [plugin-ci-template.md](./plugin-ci-template.md).

## Rules

1. Depend on `@opoha/plugin-sdk` — not core source  
2. Never edit core-owned tables  
3. No secrets in the repo — use `.env.example` only  
4. Match contract version to the host core’s expected plugin contract  

## Related

- [Using plugins](./using-plugins.md)  
- [Plugin template](./plugin-template.md)  
- [API reference](./api-reference.md)  
- `@opoha/plugin-sdk` README  
