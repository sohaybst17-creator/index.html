# AquaFarm Pro — Software Architecture

**Status:** Approved foundation for Step 1.  
**Scope:** This document defines the production architecture. It intentionally does not create the database schema, application code, mobile application, or AI implementation; those are the gated Steps 2–6.

## 1. Product and quality objectives

AquaFarm Pro is a multi-tenant aquaculture operating system for cage fish farms. It supports owners, managers, aquaculture experts, workers, and investors across web, Android, iOS, and installable PWA clients.

The system is designed around these non-negotiable qualities:

- **Tenant isolation:** a company never reads or mutates another company's data.
- **Operational correctness:** stock, biomass, feed, mortality, inventory, and financial entries are traceable and cannot silently drift.
- **Offline-tolerant field work:** workers can capture feeding, sampling, mortality, and water-quality observations with later synchronization.
- **Near-real-time awareness:** material operational events and alerts reach subscribed users quickly.
- **Internationalization:** English, Persian, Kurdish, and Arabic are first-class; RTL layout is supported for Persian, Kurdish (where configured), and Arabic.
- **Auditability:** every sensitive action has an immutable, tenant-scoped audit trail.
- **Scalability:** the platform can serve thousands of farms while preserving predictable tenant boundaries and performance.

## 2. System context

```text
Web app / PWA / Native mobile
          |
          | HTTPS + WebSocket
          v
 CDN / WAF / Load balancer
          |
          v
     Next.js 15 application (BFF presentation layer)
          |
          | REST/JSON + authenticated WebSocket gateway
          v
       NestJS modular API
          |--------------------|---------------------|
          v                    v                     v
     PostgreSQL            Redis              Supabase Storage
  source of truth     cache, queues,       documents/photos/videos
                      rate limits
          |
          v
 Analytics / AI workers ----> notification providers and report exports
```

Mapbox is consumed only by the client map module using scoped public tokens. All business data, authorization decisions, and signed storage URLs are issued by the NestJS API.

## 3. Repository and deployment topology

The target repository is a TypeScript monorepo managed with pnpm workspaces and Turborepo:

```text
apps/
  web/                 Next.js 15 app: dashboard, PWA, BFF routes
  api/                 NestJS HTTP API and WebSocket gateway
  worker/              BullMQ consumers: reports, imports, forecasts, notifications
  mobile/              React Native/Expo client (created in Step 5)
packages/
  api-contract/        Versioned DTOs, error codes, OpenAPI-generated client
  domain/              Pure domain types, calculations, policies, events
  ui/                  Accessible design system and localized primitives
  i18n/                Message catalogs, locale and RTL configuration
  config/              Shared ESLint, TypeScript, Tailwind, test configuration
  observability/       Logging, tracing, metrics conventions
infra/
  docker/              Local and production container definitions
  terraform/           Cloud infrastructure and secret references
  github/              CI/CD workflow definitions
docs/                  Architecture decision records and runbooks
```

Production runs stateless `web`, `api`, and `worker` containers independently. They scale horizontally behind a load balancer. PostgreSQL is managed, multi-AZ, point-in-time-recovery enabled; Redis is managed with persistence appropriate for queues. Supabase Storage is private by default. Infrastructure is provisioned declaratively and secrets are injected from a managed secret store, never committed.

## 4. Backend architecture

NestJS uses modular clean architecture. Each business module owns its use cases and exposes a stable application interface; no module reaches into another module's Prisma repository directly.

```text
transport (REST controllers, WebSocket handlers, import adapters)
  -> application (commands, queries, DTO validation, transactions)
    -> domain (entities, value objects, policies, domain events)
      -> infrastructure (Prisma repositories, Redis, storage, external providers)
```

### Bounded contexts

| Context | Responsibilities |
| --- | --- |
| Identity & access | users, sessions/JWT, RBAC permissions, MFA-ready security controls, company membership |
| Organization | companies, farms, lakes, cages, production cycles, species and stock lifecycle |
| Husbandry | daily feeding, sampling, growth calculations, mortality, diseases, treatment, vaccination, water quality and weather |
| Inventory & assets | feed/medicine/equipment lots, purchases, consumption, boats, nets, maintenance, suppliers |
| Workforce | employees, attendance, tasks, performance and payroll inputs |
| Finance & commerce | expenses, income, harvest, sales, customers, profitability and ROI reporting |
| Intelligence | prediction inputs/outputs, model versioning, confidence, recommendations and explainability |
| Communication | in-app, push, email and SMS notifications, subscriptions and delivery records |
| Content & compliance | documents, photos, videos, exports, imports, audit logs and retention policies |
| Reporting | read models, scheduled reports, PDF/Excel/CSV generation and comparison analytics |

Cross-context state changes are published as versioned domain events through an outbox table. A worker consumes events idempotently to update analytics read models, trigger AI evaluations, create notifications, and produce exports. Commands are transactional; charts and dashboards read denormalized, refreshable projections rather than recalculating operational history on every request.

## 5. Data architecture principles

PostgreSQL is the authoritative relational system of record. Step 2 will supply the normalized Prisma/PostgreSQL schema using these rules:

- Every tenant-owned record has `company_id`; authorization scopes it before lookup and mutations.
- UUID primary keys, UTC timestamps, actor identifiers, optimistic-lock/version fields where concurrent edits are material, and soft deletion only where recovery is a business need.
- Operational events are append-oriented. Corrections are explicit adjustment/reversal records, never destructive rewrites of historical feed, mortality, stock, inventory, or finance facts.
- Reference/master data (species, feed products, disease catalogues, permissions) is separated from tenant-owned operational data.
- Foreign keys, database checks, unique constraints, and transaction boundaries enforce invariants; application validation supplements rather than replaces them.
- Time-series tables (water quality, weather, observations, feeding) use composite tenant/farm/cage/time indexes and are partitioned by time when volume thresholds justify it.
- Derived measures—biomass, survival, FCR, SGR, ADG, stock balance, and profit—retain their source inputs and calculation/version metadata for reproducibility.
- Row-level security is evaluated as defense in depth after API tenant authorization. Backups are encrypted and restoration is tested on a schedule.

Redis is not a source of truth. It provides cache-aside reads, BullMQ queues, distributed rate limits, short-lived presence, and WebSocket fan-out coordination. Cache invalidation is driven by domain events.

## 6. API, realtime, and integration design

- Version REST APIs under `/api/v1`; publish OpenAPI contracts and generate typed clients.
- Use cursor pagination, field filters, stable sorting, and explicit date/farm/cage scopes for all collection endpoints.
- Require idempotency keys for offline-synced and financially or inventory-material commands.
- Use Zod at client boundaries and NestJS DTO validation on the server; domain policies remain the final guard.
- WebSocket channels are authenticated and tenant/farm-scoped. Event payloads carry an event ID and version so clients can de-duplicate and recover via REST.
- Long-running work (Excel import validation, report generation, media processing, bulk notifications, forecasts) runs in workers, returning a tracked job ID rather than holding an HTTP request open.
- Excel imports use a staged workflow: upload → template/version validation → row-level validation preview → user confirmation → transactional/idempotent apply → exception report and audit log.
- Exports are asynchronous, access-scoped, time-limited signed downloads with generated-at data provenance.

## 7. Frontend and experience architecture

The Next.js app uses the App Router, server components for secure initial reads, React Query for client-side server state, React Hook Form + Zod for forms, and ECharts for analytical visualizations. A reusable `packages/ui` implementation follows shadcn/ui primitives with design tokens, keyboard navigation, semantic labels, reduced-motion support, and chart/table empty, loading, offline, and error states.

Core application shells are role-aware: global command/search, farm switcher, alert center, responsive sidebar, workspace header, and context-preserving filters. Every operational workflow favors a focused, fast data-entry surface for field use while providing an expert detail view for analysis. Mapbox cage markers use accessible lists as an equivalent non-map interaction path.

Localization is message-key based, never hard-coded copy. Locale determines formatting, translation catalog, and `dir`; visual components use logical CSS properties so RTL requires no duplicate layouts. Theme preference supports system, light, and dark modes and is persisted per user.

The PWA includes a manifest, service worker, versioned asset caching, an encrypted/controlled local operation queue, conflict presentation, and background synchronization when the platform permits it. It never treats a queued field entry as authoritative until the API acknowledges it.

## 8. Security and governance

- Short-lived access JWTs and rotating, revocable refresh sessions; secure HTTP-only cookie strategy for web, secure platform storage for mobile.
- Permission checks are policy-based (`company`, `farm`, and resource scope), default-deny, and enforced in server use cases—not only in navigation.
- Passwords use a modern adaptive hash; MFA, SSO, account recovery, device/session management, and suspicious-login controls are planned extension points.
- TLS in transit, encrypted databases/backups/storage at rest, scoped Supabase signed URLs, content type/size validation, malware scanning for uploads, and no public bucket listing.
- Structured logs redact credentials, tokens, personal identifiers, and sensitive health/financial fields. Audit records capture actor, tenant, action, entity, before/after summaries, correlation ID, IP/device context, and timestamp.
- Rate limiting, request size limits, CORS/CSRF protection appropriate to client type, security headers, dependency scanning, SAST, image scanning, and secret scanning are mandatory CI controls.

## 9. Reliability, observability, and operations

Each request, job, and event has a correlation ID propagated across API, worker, logs, audits, and notifications. OpenTelemetry traces, structured JSON logs, and metrics cover latency, error rate, queue age/failure, WebSocket connections, cache hit ratio, import/export status, and business-critical anomaly processing. Alerts route to on-call based on defined SLOs.

Initial service objectives: 99.9% monthly availability for core reads/writes, p95 API reads below 400 ms under normal load, and durable acceptance of field commands before asynchronous work begins. Disaster recovery targets and retention values are finalized during infrastructure design; backups, restore drills, migration rollback plans, and incident runbooks are required before production launch.

## 10. Delivery controls and progression gate

CI runs formatting, linting, type checks, unit tests, API contract tests, database migration tests, integration tests, accessibility checks, end-to-end critical-path tests, dependency/security scans, and container builds. CD promotes immutable images through development, staging, and production with migration gating, health checks, rollback, and feature flags.

The delivery order is intentionally strict:

1. **Step 1 — Architecture:** this document establishes boundaries, quality attributes, and operating model.
2. **Step 2 — Database schema:** produce the normalized Prisma/PostgreSQL schema, migrations, seeds limited to reference data, constraints, indexes, and data dictionary.
3. **Step 3 — Backend:** implement NestJS modules, authorization, API contracts, workers, storage integration, and automated tests.
4. **Step 4 — Frontend:** implement the Next.js web/PWA application against stable contracts with production UX and accessibility.
5. **Step 5 — Mobile:** implement the native mobile client sharing contracts, domain rules, localization, and offline synchronization strategy.
6. **Step 6 — AI:** implement governed data pipelines, model services, recommendation explanations, monitoring, and human override controls.

No later step starts until the prior step is reviewed and accepted. This protects the operational data model from UI-driven shortcuts and keeps AI recommendations explainable, auditable, and safe for farm decisions.
