# ADR Lifecycle

Every ADR has a status that reflects the current state of the decision it documents. Understanding the status progression helps teams maintain their ADR collection as the system evolves.

---

## Status Values

### Proposed

The decision is under consideration. An ADR in `Proposed` status is a draft for team review. It documents a candidate decision, the context that prompted it, and the reasoning, but the decision has not yet been formally accepted.

A `Proposed` ADR is an invitation to discuss. Team members who disagree with the decision or see alternatives that were not considered should engage with the ADR at this stage.

### Accepted

The decision has been made and will be implemented or has already been implemented. An `Accepted` ADR is the primary reference for why the system is designed a particular way.

Moving an ADR from `Proposed` to `Accepted` should be a deliberate team action: a review meeting, an explicit sign-off, or a pull request approval that serves as the documented acceptance. The acceptance event and who participated should be noted when the status changes.

### Deprecated

The decision was accepted but is no longer active. The original decision is no longer in effect, but it has not been replaced by a newer decision. This status is used when a decision is reversed without a clear alternative being adopted.

### Superseded

The decision has been replaced by a newer ADR. The `Superseded` status always includes a reference to the ADR that replaces it:

```
Status: Superseded by 0007. [New Decision Title](0007-new-decision.md)
```

The original ADR is never deleted. It remains in the collection as a historical record. The chain of `Superseded` references allows future engineers to trace the evolution of a decision over time.

---

## Status Transitions

```
Proposed
    |
    v
 Accepted ---------> Deprecated
    |
    v
 Superseded (by a new ADR)
```

An ADR moves from `Proposed` to `Accepted` when the team makes the decision. It moves from `Accepted` to `Deprecated` when the decision is reversed without replacement. It moves to `Superseded` when a new ADR formalizes a different decision in the same area.

`Proposed` ADRs that are rejected do not move to a special status. They are either updated to reflect the rejection reasoning and left as `Proposed` (to document what was considered and why it was not chosen), or they are withdrawn and removed. Preserving rejected proposals with a note about why they were rejected is useful when the same idea surfaces again later.

---

## Maintaining the ADR Collection

ADRs are not living documents. Once accepted, the content of an ADR should not be changed to reflect how the decision evolved. Changes to the decision produce new ADRs, not modifications to existing ones.

The exception is minor corrections: typos, broken links, factual errors that do not affect the substance of the decision. These can be corrected directly.

If the context described in an ADR is no longer accurate because the system has changed significantly, the ADR should be superseded by a new one that documents the current state and why it differs from the previous decision.

---

## Reviewing the ADR Collection

An occasional review of the ADR collection serves the team in two ways: it identifies ADRs that should be superseded because the underlying system has changed, and it confirms that accepted ADRs are still reflected in the actual system design.

A useful trigger for collection review: when a significant architectural change is being planned. Before designing the change, review which accepted ADRs are affected. Decisions that the planned change will reverse or modify should be identified and the corresponding new ADRs drafted as part of the planning process, not after implementation.
