# AquaFarm Pro — Data Model (Step 2)

`prisma/schema.prisma` is the canonical, normalized PostgreSQL model for the platform. It is deliberately designed for migrations and a production database—not as an in-memory dashboard model.

## Aggregate map

```text
Company
 ├─ CompanyMember ─ User ─ Role ─ Permission
 ├─ Farm ─ Lake ─ Cage ─ FishStock ─ {Sampling, GrowthRecord, DailyFeeding,
 │                                   Mortality, Treatment, Vaccination, Harvest}
 ├─ Farm ─ {Employee ─ Attendance, Task, Asset ─ Maintenance}
 ├─ InventoryLot ─ InventoryMovement
 ├─ {Supplier, Customer ─ Sale ─ Harvest, Expense, Income}
 └─ {Notification, MediaAsset, AiAnalysis, AuditLog}
```

## Modelling decisions

- **Tenant boundary:** `Company` is the tenancy root. Tenant-scoped business records are reached from a company-owned aggregate, and directly scoped records retain `companyId` for authorization and efficient filtering. API policies must always require the authenticated company scope.
- **Fish lifecycle:** `FishStock` is a cage batch, rather than a mutable cage total. Sampling weights create a `Sampling`; its calculated result is an immutable `GrowthRecord`. Feed, mortality, treatment, vaccination, and harvest link to the exact stock batch.
- **Inventory ledger:** `InventoryLot` represents a traceable feed, medicine, or equipment lot; `InventoryMovement` is append-only. Current stock is calculated from movements, preventing destructive adjustments from losing provenance.
- **Finance:** expenses/income are independent financial facts. Harvest and sale quantities/prices remain separate from accounting entries so financial approvals and operational events can evolve independently.
- **Evidence and AI:** media objects only retain private object-storage metadata. AI output stores input hash, model version, confidence, result, state, and timestamps so a recommendation is reproducible and auditable.
- **Time series:** water quality, weather, daily feeding, mortality, growth, and inventory movements have descending timestamp indexes for cage/stock operational views. Step 3 must add monthly PostgreSQL partitions for high-volume telemetry once real workload thresholds are measured.

## Integrity requirements implemented by the schema

1. UUID IDs, UTC `DateTime` values, foreign keys, required relations, and uniqueness constraints protect identity and tenancy relationships.
2. A user can have only one membership per company; a role-to-permission grant is unique; cage codes are unique within a lake; stock batch codes are unique in a cage.
3. A sampling can create no more than one growth record, and only one growth record exists per stock/timestamp.
4. Attendance is unique per employee/work date; maintenance is related to either a cage or an asset at application validation time.
5. Check constraints that Prisma cannot express—positive counts/amounts, valid latitude/longitude, non-empty inventory movements, and exactly-one maintenance target—must be added in the initial SQL migration during backend delivery.

## Migration and access policy

Before application deployment, create reviewed Prisma migrations from this schema, enable the PostgreSQL `citext` extension, add the SQL checks above, and apply migrations with `prisma migrate deploy`. The NestJS application connects with a non-owner application role. A separate migration role owns DDL; database row-level security policies are added as defense in depth using the request's company context.

No operational seed data is included. Only global reference data—such as standard permissions, supported species, and disease catalogues—may be seeded and must be versioned separately from customer data.
