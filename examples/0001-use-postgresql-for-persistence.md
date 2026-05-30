# 0001. Use PostgreSQL for Application Persistence

**Date:** 2026-06-02
**Status:** Accepted
**Deciders:** Engineering Lead, Backend Team

---

## Context

The application requires persistent storage for user accounts, workflow state, audit logs, and configuration data. The data model involves structured records with defined relationships between entities. Audit requirements mean the system needs reliable transaction semantics: operations must either complete fully or not at all.

The team is evaluating options at a stage where the data model is reasonably well understood and the primary risk is operational reliability, not schema flexibility.

Three options were considered:

PostgreSQL (relational), MongoDB (document store), and DynamoDB (managed key-value with document support).

Team size is small. Operational overhead is a significant factor. No member of the current team has production operations experience with MongoDB or DynamoDB at the scale this system will reach. All members have PostgreSQL production experience.

---

## Decision

Use PostgreSQL as the primary persistence layer for all application data at launch.

---

## Rationale

PostgreSQL provides the transaction semantics the audit requirements demand without additional application-level coordination. ACID compliance is native to the database, not something the team needs to build on top of.

The relational model fits the current data shape well. The core entities (users, workflows, audit events, configurations) have clear relationships. A document store would require the team to manage join logic in application code that PostgreSQL handles at the query level.

DynamoDB would reduce operational overhead for infrastructure but increases the complexity of query patterns that are important for this use case. Access patterns for audit log retrieval and workflow state queries are not easily modeled as single-table designs without significant schema investment upfront.

MongoDB was rejected because the flexible schema model is not an advantage here. Schema flexibility tends to produce schema divergence over time in teams without dedicated schema governance. Enforced schema at the database level is a constraint that helps this use case, not a limitation.

The team's operational familiarity with PostgreSQL is not a tiebreaker. It is the deciding factor given current team size. Debugging production issues in a database system the team understands well is significantly less expensive than learning operational failure modes under pressure.

---

## Consequences

### Positive
- ACID transactions are available without additional coordination at the application level
- Complex queries for audit log retrieval and workflow state analysis can be expressed in SQL without application-level aggregation
- The team can operate the database in production without a learning curve during early incidents
- Managed PostgreSQL options (RDS, Supabase, Neon) reduce infrastructure overhead while keeping the operational model familiar

### Negative / Trade-offs
- Horizontal write scaling requires additional work (read replicas, connection pooling, eventually sharding if volume demands it). This is a future problem, not a current one, but the team should not assume the current architecture scales to very high write volumes without architectural changes
- Schema migrations require careful management as the data model evolves. The expand-contract pattern for migrations should be adopted as a team practice early, before the first migration that would require downtime
- If the data model evolves significantly toward document-like structures or unstructured data, this decision should be revisited

### Neutral
- JSONB columns in PostgreSQL provide document-store-like flexibility for fields that benefit from it, allowing the team to handle semi-structured data without migrating off PostgreSQL

---

## Implementation Notes

Connection pooling should be configured from the start rather than added later. PgBouncer or the pooling provided by the managed service should be in place before the first load test.

Migration tooling should be selected and standardized before the first schema change. Flyway, Liquibase, or framework-native migration tools are all acceptable. The tooling matters less than the convention: migrations are committed alongside the code that requires them, reviewed in pull requests, and never run manually against production.

---

## Related Decisions

- Will inform: database migration strategy (future ADR)
- Will inform: connection pool configuration (future ADR)
