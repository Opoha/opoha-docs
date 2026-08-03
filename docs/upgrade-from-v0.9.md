# Upgrade from v0.9 to v1.0

Move an Opoha app from **v0.9 (Automation)** to **v1.0 (Stable Release)**. Persistence remains **TypeORM** (ADR-0010). Admin and storefronts talk to core **only** through GraphQL.

Canonical workspace authority (planning detail + migration table): `opoha-workspace/docs/readiness/upgrade-guide-v0.9-to-v1.0.md`.

## What changes

| Area | Impact |
|------|--------|
| Packages | Stage / pin `@opoha/*@1.0.0` (publish is separate / user-gated) |
| Database | Run pending TypeORM migrations (jobs, rules, webhooks if lagging) |
| GraphQL | No field removals in this jump; future removals need a one-minor deprecation window |
| Plugins | Keep `contractVersion: "0.1"`; bump plugin packages to `1.0.0` with core |
| Env | Same keys; production `opoha doctor` enforces strong JWT, no seed password, non-default DB |

## Upgrade steps

1. **Backup** Postgres (`pg_dump`).
2. **Install** `@opoha/core@1.0.0`, `@opoha/sdk@1.0.0`, `@opoha/cli@1.0.0`, Admin/plugins as needed (`pnpm install`).
3. **Review** `.env` against `opoha-core/.env.example` (`DATABASE_URL`, `REDIS_URL`, `JWT_SECRET`, plugin paths, optional `OPOHA_JOB_QUEUE`).
4. **Migrate:** `pnpm migrate` (TypeORM).
5. **Verify:**
   ```bash
   pnpm exec opoha doctor
   # optional spine smoke (local multi-repo):
   cd opoha-core && SKIP_DOCKER=1 pnpm walking-skeleton
   ```
6. **Deploy** per [deployment.md](./deployment.md).

## Plugins

- Official plugins certify against core `1.x` — see workspace `official-plugin-matrix.md`.
- Peer on `@opoha/plugin-sdk@^1.0.0`.
- Do **not** bump `contractVersion` unless the manifest schema itself breaks (it stays `"0.1"` at package `1.0.0`).

## GraphQL clients

- Send `X-API-Version: 1` (or omit for default `1`).
- Prefer `PaymentCaptured` over the kept `PaymentSucceeded` alias.
- Follow the workspace GraphQL deprecation policy before removing client fields post-1.0.

## Related

- [Getting started](./getting-started.md)
- [Deployment](./deployment.md)
- [Plugin author guide](./plugin-author-guide.md)
- [API reference](./api-reference.md)
