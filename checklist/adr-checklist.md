# ADR Checklist

A quick check before an ADR is shared for review and before it is accepted. It is not a substitute for [the review process](../docs/adr-review-process.md); it is the fast pass that catches the common gaps.

## Before sharing for review (Proposed)

- [ ] The decision is stated in a sentence or two, unambiguously.
- [ ] The context describes the forces and constraints as they are, not as they should be.
- [ ] The alternatives that were seriously considered are named, with why each was set aside.
- [ ] The rationale captures the reasoning a future engineer could not reconstruct from the code.
- [ ] The consequences list the trade-offs, not just the benefits.
- [ ] Any assumptions the decision rests on are written down (load, team size, product direction).
- [ ] It captures one decision. A second decision belongs in its own ADR.
- [ ] The file is numbered sequentially and titled in kebab-case, and the status is Proposed.

## Before accepting (Accepted)

- [ ] The people who need to weigh in have, and their concerns are reflected or answered.
- [ ] The trade-offs are understood and accepted, not glossed over.
- [ ] If this reverses or changes an earlier decision, that ADR is referenced and its status updated.
- [ ] The status is set to Accepted with the date, and the deciders are named.

## The test

Would a senior engineer joining in six months understand, from this record alone, what was decided and why, without finding the person who made the call? If yes, the ADR is doing its job.
