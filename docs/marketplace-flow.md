# Marketplace flow (v0.7)

Discover and install Opoha plugins via the **JSON registry catalog** — no Opoha Cloud billing, no core TypeORM registry tables (ADR-0010).

**Canonical catalog:** `@opoha/cli` `src/registry/` (schema + built-in default).  
**Admin browse:** `/marketplace` in `@opoha/admin` (same catalog shape; optional remote URL).  
**Workspace readiness:** see `opoha-workspace` `docs/readiness/marketplace-flow.md`.

## Flow

```text
catalog URL or file
  → opoha plugin search <query> [--registry <url|path>]
  → opoha plugin install <id> [--registry …] [--core-version <semver>]
  → .opoha/plugins.lock.json
```

Admin staff can also **browse** the catalog at `/marketplace` (channel, verified, contract / core-range badges). Install remains CLI for v0.7.

## Commands

```bash
# Built-in catalog
pnpm exec opoha plugin search sample
pnpm exec opoha plugin search payment --channel official

# File or HTTP catalog
pnpm exec opoha plugin search sample --registry ./catalog.json
pnpm exec opoha plugin search sample --registry https://example.com/opoha-catalog.json

# Install compatible version (pathHint → local sibling for v0.7)
pnpm exec opoha plugin install sample --core-version 0.7.0
pnpm exec opoha plugin install sample --registry ./catalog.json --core-version 0.7.0
```

## Compatibility fields

Each catalog version entry includes:

| Field | Meaning |
|-------|---------|
| `contractVersion` | Must match `@opoha/plugin-sdk` contract (currently `0.1`) |
| `opohaCoreRange` | Semver range of compatible `@opoha/core` (e.g. `>=0.1.0 <0.8.0`) |

Admin badges compare these to the running contract / core version (**display only** — CLI enforces on install).

## Channels & verification

- `channel`: `official` \| `community`
- `verified`: curated boolean for v0.7 (manual catalog curation)
- Third-party proof: community `plugin-sample` (`sample`)

## Out of scope (v0.7)

- Paid marketplace settlement (Phase 10 — Opoha Cloud)
- Admin one-click install
- Signed npm provenance
