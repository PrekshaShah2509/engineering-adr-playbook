# 0002. Adopt Blue-Green Deployment Strategy

**Date:** 2026-06-02
**Status:** Accepted
**Deciders:** Engineering Lead, Infrastructure, Product

---

## Context

The application is approaching its first production deployment with real user traffic. The team needs to establish a deployment strategy that defines how code reaches production, how rollback works when something goes wrong, and how risk is managed during the deployment window.

Three approaches were evaluated:

In-place deployment (shut down old version, deploy new version, restart). Simplest to implement, highest deployment risk. Rollback requires redeployment. Appropriate for systems where brief unavailability is acceptable and deployment frequency is low.

Rolling deployment (gradually replace old instances with new ones). Reduces downtime risk but requires the application to handle two versions running simultaneously. Rollback is complex because the system is in a mixed state during deployment.

Blue-green deployment (maintain two production environments, switch traffic via load balancer routing). Zero downtime during deployment. Rollback is a routing change, not a redeployment.

The application is expected to have users in IST business hours (09:00 to 18:00). Downtime during business hours is not acceptable after launch. The product roadmap includes frequent feature releases.

---

## Decision

Adopt blue-green deployment as the standard deployment strategy for the application's production environment.

---

## Rationale

Rollback as a routing decision rather than a redeployment changes the risk profile of every release. When a problem is detected in production, the team can route traffic back to the previous version within seconds. The alternative, re-deploying the old version, takes minutes to hours and requires a known-good artifact to be available and tested.

The deployment frequency goal makes rollback speed more important over time, not less. Teams that deploy frequently rely on fast rollback as the primary risk control for each deployment. Teams that deploy infrequently tend to compensate with more elaborate pre-release testing. For a product roadmap that involves regular feature releases, the blue-green model supports the deployment cadence better.

The requirement that old and new versions coexist safely during the routing switch is a design constraint that surfaces important architectural properties. If the application cannot handle a brief period where two versions are both alive and both potentially receiving requests, that is a signal about the API contracts and database schema design. Addressing that surface early is preferable to discovering it under pressure during the first significant release.

In-place deployment was rejected because rollback as a redeployment is too slow for a system with active users during business hours. Rolling deployment was rejected because the mixed-version state adds complexity to schema migration and stateful session handling that the team would need to address immediately.

---

## Consequences

### Positive
- Rollback is a routing decision: minutes become seconds, and the team can make the call without a full deployment pipeline run
- Deployment risk is contained: a new version can be fully deployed and validated before any user traffic is routed to it
- The coexistence requirement for old and new versions is a forcing function for better API and schema design practices early

### Negative / Trade-offs
- Infrastructure cost approximately doubles during deployments. Two full environments must be maintained. For the current architecture this is manageable; at very large scale, the cost may make canary or feature-flag-based deployments more economical
- Database migrations must be backward-compatible during the transition window. An old version of the application may be reading from the same database as the new version during the brief period between deployment and traffic switch. This requires the expand-contract migration pattern (see implementation notes)
- The team needs a working health check system before blue-green routing makes sense. Routing traffic to a "green" environment that is unhealthy is worse than a failed in-place deployment. Health checks are a prerequisite, not an enhancement

### Neutral
- The same blue-green infrastructure can serve as the foundation for canary releases later, if the team wants to route a percentage of traffic to the new version rather than switching all at once

---

## Implementation Notes

Health checks must be implemented and validated before the first blue-green deployment. The load balancer should only route traffic to an environment that passes health checks. A green environment that starts up but is misconfigured is a failure mode that health checks must catch.

Database migrations during a blue-green deployment must be safe for both the current (blue) and new (green) application version to read against simultaneously. This means: columns cannot be dropped until the blue environment is decommissioned, schema changes must be additive in the first migration and cleanup happens in a subsequent release.

Deployment runbooks should specify: what the health check criteria are, how long to observe the green environment before confirming the switch, and the rollback trigger conditions (error rate threshold, latency increase, specific error types).

The deployment automation should produce an artifact that identifies the green environment as the current target and automates the routing switch, rather than requiring manual console operations. Manual steps during deployments are a source of human error under time pressure.

---

## Related Decisions

- Builds on: 0001 (PostgreSQL) — the expand-contract migration requirement is more important in a blue-green setup
- Will inform: database migration strategy (future ADR)
- Will inform: feature flag adoption (future ADR)
