# 0003. API Versioning Approach for External Consumers

**Date:** 2026-06-02
**Status:** Accepted
**Deciders:** Engineering Lead, Product

---

## Context

The application exposes an API that external consumers will integrate against. As the product evolves, the API will need to change. Some changes will add new capabilities. Some will modify existing behavior. Some will remove deprecated functionality.

Without a versioning strategy, any breaking change requires coordinated simultaneous updates across all consumers. For internal consumers this is operationally expensive. For external consumers it may be impossible.

Four approaches were evaluated:

URL path versioning (/v1/, /v2/). Clear consumer contract, simple to implement, simple to route. Versioned endpoints must be maintained until consumers migrate.

Header versioning (API-Version: 2). Cleaner URLs but less discoverable. Requires consumers to set headers correctly. More complex to test.

Query parameter versioning (?version=2). Simple but easy to omit. No strong discoverability advantage over header versioning.

Non-breaking evolution with deprecation cycles. No version segments. The API contract is maintained backward-compatibly until an explicit deprecation window passes. Consumers are not required to update until the deprecated behavior is removed.

---

## Decision

Use URL path versioning for the external API. The initial version is `/v1/`. Breaking changes will be released under `/v2/` with a defined migration window before `/v1/` is deprecated.

Within a major version, all changes must be backward-compatible: new fields can be added, optional parameters can be added, new endpoints can be added. Existing fields, required parameters, and endpoint behavior cannot be changed without a major version increment.

---

## Rationale

URL path versioning makes the consumer contract explicit and discoverable. External consumers integrating with a versioned endpoint can see the version at the URL level without reading documentation. Routing between versions at the infrastructure level is straightforward and does not require application-level version parsing.

The non-breaking evolution approach was rejected because it places the responsibility for backward compatibility entirely on the implementation team with no visible contract for consumers. When the team needs to make a breaking change, the lack of versioning makes the migration more disruptive than it would be under URL versioning.

Header versioning was rejected because it is less discoverable and requires documentation review for consumers to use correctly. The discoverability advantage of URL versioning is worth the slightly less clean URL structure.

The major-version-only approach (changes within a version are backward-compatible) reduces version proliferation. Teams that version at the endpoint level or at the minor version level tend to produce version sprawl that increases maintenance burden and consumer confusion.

---

## Consequences

### Positive
- External consumers have a stable contract. Integrating against `/v1/` means the consumer will not be broken by internal changes until `/v1/` is formally deprecated with a defined timeline
- Breaking changes have a visible migration path. `/v2/` runs alongside `/v1/` during the migration window. Consumers can migrate on their own timeline within the window
- Infrastructure-level routing between versions is simple and observable

### Negative / Trade-offs
- Maintaining multiple major versions in parallel is operationally expensive if the migration window is long. The team must decide on a deprecation timeline policy before the first major version increment. A 90-day migration window is a reasonable starting point for external consumers
- Backward compatibility within a major version constrains the team's ability to fix design mistakes. A field that was named incorrectly or a response structure that is poorly designed must be carried until the next major version. This makes the initial API design more consequential than it would be under a more liberal versioning approach
- Versioned endpoints require routing configuration, endpoint duplication, and test coverage maintained for each active version. This cost scales with the number of active major versions and the surface area of the API

### Neutral
- The versioning contract applies to the external API. Internal service-to-service APIs can follow a different convention if the deployment cadence and consumer coordination model supports it

---

## Implementation Notes

A deprecation policy should be documented before the first major version increment is released. The policy should specify: the minimum migration window for external consumers (recommended 90 days), how deprecation is communicated (response headers, API documentation, direct consumer notification), and what happens after the deprecation window closes.

Each major version should have a changelog maintained alongside the code. The changelog should document what changed between versions and why, with enough context for a consumer to understand the migration impact without reading the source code.

The `/v1/` base path should be set in a configuration layer that can be updated for routing, rather than hardcoded throughout the application. This simplifies version management as the API surface grows.

---

## Related Decisions

- Related: 0002 (blue-green deployment) — API backward compatibility within a major version is a requirement for the coexistence window during blue-green deployments
- Will inform: deprecation policy (future ADR)
