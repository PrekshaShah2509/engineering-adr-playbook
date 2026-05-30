# Engineering ADR Playbook

Architecture decisions get made in planning sessions and forgotten in team transitions.

A year later, no one knows why the system was designed a particular way. The reasoning is in someone's head, a Slack thread, or nowhere. The decision gets relitigated, sometimes made differently, and the system accumulates assumptions that were never made visible.

This playbook provides a structured approach to capturing architecture decisions as they happen, using Architecture Decision Records (ADRs).

---

## What an ADR Is

An ADR is a short document that captures a significant architecture decision: the context that made the decision necessary, the decision itself, the reasoning behind it, and the trade-offs it introduces.

It is not a design document. It is not a specification. It is a record that future engineers can read to understand why the system is the way it is, without having to find the person who made the call.

---

## Quick Start

1. Copy `templates/0000-adr-template.md` into the `decisions/` folder of your repository (or wherever your team stores ADRs)
2. Rename it with a sequential number and a short title: `0001-use-postgresql-for-persistence.md`
3. Fill in the context, decision, rationale, and consequences sections
4. Set the status to `Proposed` and share it for team review
5. Update status to `Accepted` once the decision is made

See [docs/adr-lifecycle.md](docs/adr-lifecycle.md) for the full status progression.

---

## What Is in This Repo

```
templates/
  0000-adr-template.md        Standard ADR template
  0000-lightweight-adr.md     Shorter template for lower-stakes decisions

examples/
  0001-use-postgresql-for-persistence.md    Database selection decision
  0002-blue-green-deployment-strategy.md    Deployment architecture decision
  0003-api-versioning-approach.md           API contract management decision

docs/
  when-to-write-an-adr.md     Decision criteria for what warrants an ADR
  adr-lifecycle.md             Status transitions and governance
  adr-review-process.md        How to run an ADR review as a team
```

---

## When to Write an ADR

Not every decision needs a record. The ones that do tend to share certain characteristics: they are hard to reverse, they carry assumptions the team will need to understand later, or they affect how the system can evolve.

See [docs/when-to-write-an-adr.md](docs/when-to-write-an-adr.md) for a more detailed decision guide.

As a starting point, consider writing an ADR for:

- Technology selection decisions (databases, frameworks, infrastructure)
- Architectural patterns with organizational implications (microservices boundaries, event-driven designs, API contracts)
- Decisions that reject a seemingly obvious approach for non-obvious reasons
- Changes to decisions that were previously captured in an ADR

---

## Template Overview

```markdown
# [NNNNN]. [Title]

Date: YYYY-MM-DD
Status: Proposed | Accepted | Deprecated | Superseded by NNNNN
Deciders: [Names or roles]

## Context
## Decision
## Rationale
## Consequences
```

See [templates/0000-adr-template.md](templates/0000-adr-template.md) for the full template with guidance.

---

## Naming Convention

ADR files are numbered sequentially with four or five digits and a short descriptive title in kebab-case:

```
0001-use-postgresql-for-persistence.md
0002-blue-green-deployment-strategy.md
0003-api-versioning-approach.md
```

Numbering is sequential and permanent. ADRs are never renumbered. When a decision is reversed or superseded, a new ADR is created that references the original.

---

## Storing ADRs

The recommended location is a `decisions/` folder at the root of the repository the decision applies to. For decisions that span multiple repositories, a dedicated ADR repository works well.

What matters less is where you store them. What matters more is that they are version-controlled, discoverable, and reviewed as part of the same workflow as the code they describe.

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidance on proposing changes to the templates or process.

---

Built to support engineering teams that treat decision discipline as an operational practice, not a documentation exercise.
