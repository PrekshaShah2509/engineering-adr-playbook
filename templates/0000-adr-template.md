# [NNNNN]. [Short Title]

**Date:** YYYY-MM-DD
**Status:** Proposed
**Deciders:** [Names or roles of people involved in this decision]

---

## Context

What is the situation that makes this decision necessary? Describe the technical or organizational forces at play, the constraints that exist, and what problem is being addressed.

Keep this section factual and neutral. It should describe the state of the world as it is, not as it should be. The decision that follows should feel like a logical response to this context.

Examples of context worth capturing:
- Current system behavior that this decision changes
- Constraints imposed by existing infrastructure, team size, or operational requirements
- Alternative approaches considered and why they were not chosen
- External factors: compliance requirements, performance targets, cost limits

---

## Decision

State the decision clearly. A single sentence or short paragraph is usually sufficient.

"We will use X" or "We have decided to adopt Y" or "The team has chosen to reject Z in favor of W."

This section should be unambiguous about what was decided. The reasoning belongs in Rationale.

---

## Rationale

Why was this decision made? What made this option preferable to the alternatives?

This is the most important section. Future engineers reading this record will understand the decision from the Decision section. What they cannot reconstruct without this record is the reasoning.

Capture:
- What alternatives were seriously considered
- Why each alternative was rejected
- What assumptions or predictions underlie this decision
- What would need to change for this decision to be revisited

---

## Consequences

### Positive
What becomes easier, faster, safer, or more reliable because of this decision?

### Negative / Trade-offs
What becomes harder? What new problems does this decision introduce? What capabilities does the team give up?

Trade-offs are not reasons to avoid the decision. They are information future engineers need to understand the system.

### Neutral
What changes without being clearly better or worse?

---

## Implementation Notes

*(Optional)* Any specific guidance relevant to implementing this decision. Links to relevant documentation, migration steps, or deprecation timelines.

---

## Related Decisions

*(Optional)* References to other ADRs that this decision builds on, supersedes, or is in tension with.

- Supersedes: [NNNNN. Title](../decisions/NNNNN-title.md)
- Related: [NNNNN. Title](../decisions/NNNNN-title.md)
