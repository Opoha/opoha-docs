# Using plugins

Enable and develop Opoha plugins without putting plugin paths in `.env`.

## Source of truth: `opoha.config.json`

```json
{
  "name": "my-store",
  "plugins": [
    "@opoha/plugin-manual-payment",
    "@opoha/plugin-shipping-flat-rate",
    "./plugins/my-local-plugin"
  ]
}
```

Each entry is an npm package name (from `node_modules`) or a filesystem path to a plugin root.

Day-to-day plugin management belongs in this file (and `opoha plugin install|remove`).  
`OPOHA_PLUGINS` / `OPOHA_PLUGINS_PATH` are **optional overrides** for CI or temporary experiments.

## Add an official plugin

```bash
pnpm add @opoha/plugin-stripe
# Add "@opoha/plugin-stripe" to opoha.config.json "plugins", or:
pnpm exec opoha plugin install stripe --core-version 1.0.0
pnpm dev
```

Restart the API after changing the list.

## Develop a local plugin

```bash
pnpm exec opoha generate plugin my-widget
cd my-widget && pnpm install && pnpm build
cd ../my-store
pnpm exec opoha plugin install ../my-widget
pnpm exec opoha plugin list
pnpm dev
```

Build plugins against `@opoha/plugin-sdk` only — do not import `@opoha/core`.

## Where plugins appear

| Surface | What you get |
|---------|----------------|
| Boot logs | `Plugins discovered: …` |
| GraphQL | `plugins` query; payment/shipping/tax/… providers the plugin registered |
| Admin | Navigation and pages from `registerAdmin` |

## Related

- [Getting started](./getting-started.md)
- [Plugin author guide](./plugin-author-guide.md)
- [Plugin template](./plugin-template.md)
