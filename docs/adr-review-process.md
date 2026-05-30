# ADR Review Process

An ADR is a team document, not an individual one. The review process is what gives it authority as a decision record.

---

## Who Should Review

The review participants depend on the scope of the decision. A useful starting point:

- The engineer or engineers who will implement the decision
- The engineering lead or technical lead responsible for the area affected
- Anyone whose system will be affected by the decision (upstream or downstream services, shared infrastructure, platform teams)
- A product representative when the decision has product implications (API contracts, data model changes that affect features)

Not every ADR requires a large review. A decision that affects only a single service and has limited downstream implications can be reviewed by a small group. A decision that establishes a pattern for the whole engineering organization warrants broader participation.

---

## Review Workflow

**Step 1: Author creates a draft ADR**

The author creates the ADR with status `Proposed` and commits it to version control (or creates it in whatever system the team uses for ADR storage). The draft should be complete enough that reviewers can evaluate the decision without needing additional context documents.

**Step 2: Author requests review**

The review request is explicit. A pull request comment, a Slack message, a meeting invite: the format is less important than the clarity that a decision is being proposed and feedback is needed by a specific date.

The review period should be long enough for reviewers to read and think carefully about the decision. One to three business days is a reasonable minimum for most decisions. Larger decisions with broader organizational impact warrant more time.

**Step 3: Reviewers engage**

Reviewers who have concerns, see alternatives that were not considered, or disagree with the decision should raise these during the review period. The ADR should be updated to reflect alternatives that were raised and why they were accepted or rejected.

Reviewers who have no concerns after reading should indicate that explicitly. "No concerns" is useful feedback. Silence is ambiguous.

**Step 4: Decision is made**

The team reaches a decision: accept the proposal, reject it, or revise it and circulate a new draft. The decision should be made explicitly, not assumed from inaction.

For accepted decisions, the ADR status changes from `Proposed` to `Accepted`. The date of acceptance and the participants should be noted in the ADR or in the pull request that changes the status.

**Step 5: ADR is merged and linked**

The accepted ADR is merged into the main branch and linked from relevant documentation: the service README, the architecture documentation, or wherever the team maintains its engineering context.

---

## Asynchronous vs. Synchronous Review

Most ADR reviews can be conducted asynchronously through pull request comments or document comments. Synchronous review meetings are appropriate when:

- The decision is high-stakes and involves multiple teams with potentially conflicting interests
- The written discussion has reached an impasse and real-time dialogue would resolve it faster
- The decision needs to be made on a timeline that does not allow for async back-and-forth

When a synchronous review meeting is held, the decisions made and the reasoning discussed should still be captured in the ADR. A meeting that produces a decision but leaves no written record of the reasoning defeats the purpose of the ADR process.

---

## When There Is Disagreement

Disagreement during ADR review is a healthy sign that the decision is non-trivial and the alternatives were worth considering.

The goal of the review process is not consensus but informed decision-making. When reviewers disagree, the review discussion should surface the reasoning on each side. The ADR can document the disagreement explicitly: "Option X was advocated for by [role] because [reasoning]. This proposal was not adopted because [reasoning for the accepted decision]."

Documenting the disagreement is particularly valuable for decisions that were close calls. Future teams revisiting the decision will benefit from knowing that the alternative was seriously considered and why it was not chosen.

An ADR that was accepted over significant objection should note the objection and what would need to change for the objection to be resolved. If the conditions change, the objection provides a basis for revisiting the decision.

---

## Lightweight Reviews for Lower-Stakes Decisions

Not every decision requires a formal multi-step review. For decisions that are lower-stakes, clearly reversible, or fall within the established technical direction of the team, a lighter review is appropriate.

Use the lightweight ADR template. Share it with one or two relevant reviewers with a short turnaround window. Merge with minimal ceremony.

The appropriate weight of the review should match the cost of being wrong about the decision.
