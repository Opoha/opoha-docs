# Plugin author CI template

Canonical GitHub Actions workflow shipped with `opoha generate plugin`.

**Source of truth:** `opoha-cli/templates/plugin/.github/workflows/ci.yml`

## What it runs

On `push` and `pull_request`:

1. Checkout  
2. Setup Node 20 + pnpm  
3. `pnpm install`  
4. `pnpm typecheck`  
5. `pnpm test`  
6. `pnpm build`  

## Using it

- Generated plugins include the workflow automatically.  
- For hand-authored plugins, copy `.github/workflows/ci.yml` from a fresh `opoha generate plugin` output.  
- When using `--link` / `file:` `@opoha/plugin-sdk`, CI must either publish the SDK first or substitute a registry version before `pnpm install`.

## Related

- [Plugin author guide](./plugin-author-guide.md)  
- [Plugin template](./plugin-template.md)  
