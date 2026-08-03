# Analytics storefront hooks (stub)

Phase 4 content for GA4 / Meta Pixel integration.

**Canonical contract:** see `opoha-workspace` docs:

- `docs/design/analytics-events-design.md`
- `docs/design/analytics-storefront-integration.md`

## Summary

- Subscribe to Opoha domain events (`CartLineAdded`, `CheckoutPrepared`, `OrderPaid`, …).
- Map via `ANALYTICS_STOREFRONT_MAP` from `@opoha/core`.
- Never load provider SDKs inside the commerce engine.
- Register a sink once via `AnalyticsSinkRegistry` (event-bus module) and the `AnalyticsSinkDispatcher` forwards every cataloged event automatically — this is the F-04 "storefront hook package", implemented as a core registration API (no dedicated `plugin-analytics` repo needed for v0.5).

Full pages arrive when the docs site tooling ships.
