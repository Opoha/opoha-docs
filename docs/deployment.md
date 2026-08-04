# Deployment guide

Operate Opoha core in a production-like environment. Persistence remains **TypeORM** (ADR-0010). Admin and storefronts talk to core **only** through GraphQL.

## Architecture reminder

| Layer | Role |
|-------|------|
| `opoha-core` | NestJS + Apollo GraphQL + TypeORM host + plugin loader |
| Postgres | Primary store (migrations via TypeORM) |
| Redis | Jobs / cache surfaces as configured |
| Plugins | Loaded via `@opoha/plugin-sdk` contracts — never import `@opoha/plugin-*` from core source |

## Environment

Copy `.env.example` → `.env` (or inject via your secrets manager). Never commit secrets.

| Variable | Production requirement |
|----------|------------------------|
| `NODE_ENV` | `production` |
| `DATABASE_URL` | Real Postgres credentials — **not** default docker `opoha:opoha` |
| `REDIS_URL` | Reachable Redis |
| `JWT_SECRET` | Strong secret, **≥ 32 characters** |
| `SEED_ADMIN_PASSWORD` | **Unset** in production |
| `PORT` | As required by your reverse proxy |
| `OPOHA_PLUGINS` / `OPOHA_PLUGINS_PATH` | Plugin roots when using local/file plugins |

Optional: `JWT_EXPIRES_IN`, `JWT_REFRESH_EXPIRES_IN`, `LOG_LEVEL`, OpenTelemetry flags per core `.env.example`.

## Release steps (typical)

1. Provision Postgres + Redis  
2. Set production env (above)  
3. `pnpm install --prod` (or your CI image install)  
4. `pnpm migrate` (TypeORM migrations)  
5. **Do not** run seed with production admin passwords from `.env` — create operators via secure process  
6. `pnpm build` / `pnpm start` (or process manager)  
7. Terminate TLS at a reverse proxy; rate-limit `login` / `refresh` at the edge (accepted residual risk — see security checklist)  
8. Run `opoha doctor` against the deployment host env  

## Doctor production checklist

With `NODE_ENV=production`, `opoha doctor` enforces:

| Check | Fail when |
|-------|-----------|
| `JWT_SECRET` present | Missing |
| `JWT_SECRET` strength | Length &lt; 32 |
| `SEED_ADMIN_PASSWORD` | Set |
| Database URL | Looks like default docker `opoha:opoha` credentials |
| Postgres / Redis TCP | Unreachable (unless connectivity skipped in tests) |
| Plugin manifests | Contract mismatch vs lockfile |

Exit **0** only when there are no failures (warnings allowed).

```bash
NODE_ENV=production pnpm exec opoha doctor
```

## Plugins in production

- Pin `@opoha/plugin-sdk` compatible range (`contractVersion` / peer dep)  
- Prefer published plugin packages or controlled `file:` installs  
- Run compatibility CI for official plugins before upgrading core  

## Related

- [Getting started](./getting-started.md)  
- [API reference](./api-reference.md)  
- Workspace: `docs/readiness/security-review-checklist.md`, `docs/qa/ac-p9-security-gate.md`  
