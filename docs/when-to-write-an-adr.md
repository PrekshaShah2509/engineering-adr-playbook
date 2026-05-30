# When to Write an ADR

The goal of an ADR is not to document everything. It is to capture decisions that would be expensive to reconstruct later.

Not every engineering decision warrants a record. The ones that do tend to share certain characteristics.

---

## Write an ADR when the decision is hard to reverse

Technology selections, architectural patterns, and API contracts are hard to change once embedded in a production system. The cost of the wrong decision compounds over time. An ADR creates a record of what made the decision reasonable at the time, which is useful both for future defenders of the choice and for future teams considering a change.

Examples:
- Choosing a primary database
- Adopting an event-driven architecture
- Deciding on an API contract model

---

## Write an ADR when the decision rejects a seemingly obvious approach

Teams often make reasonable decisions that look wrong at first glance. Choosing a relational database when document stores are popular. Adopting a monolith when the industry conversation is about microservices. Sticking with a synchronous API when the architecture team recommended messaging.

These decisions, when made deliberately, often have strong reasoning behind them. Without a record, that reasoning disappears. A future team member sees the apparently odd choice and assumes it was an oversight rather than a considered trade-off.

---

## Write an ADR when the decision carries assumptions the team will need later

Some decisions embed assumptions about load, team size, operational maturity, or product direction. Those assumptions are visible at decision time and invisible six months later.

Capturing the assumptions alongside the decision means future engineers can evaluate whether the assumptions still hold before deciding whether to revisit the choice.

Examples:
- "This approach is appropriate for our current team size of five engineers; at fifteen engineers it should be reconsidered"
- "This design assumes read-heavy workloads; if the write-to-read ratio shifts significantly, the cache invalidation strategy will need to change"

---

## Write an ADR when a previous decision is being reversed or significantly modified

A new ADR should reference the original. This creates a chain of reasoning that shows how the system's design evolved and why. Future engineers can read the chain to understand what changed and what the team learned between the two decisions.

---

## Do not write an ADR for every decision

ADR value comes from the signal-to-noise ratio. If every implementation detail gets an ADR, the important decisions become hard to find.

Skip ADRs for:
- Implementation details that are easily visible in the code
- Decisions that are easily reversible with minimal cost
- Standard practices that are already captured in team conventions or coding guidelines
- Tactical choices within an already-established architectural pattern

The test: would a senior engineer joining the team in six months need this document to understand why the system was built this way? If yes, write the ADR. If the code and conventions would answer the question, skip it.

---

## A Note on Timing

ADRs are most useful when written at decision time, before implementation begins. The context is fresh, the alternatives are still visible, and the reasoning can be captured accurately.

An ADR written after the fact is still better than no ADR. It captures the context and reasoning while people who made the decision are still available to contribute. But it is harder to write accurately and may miss alternatives that were considered but not remembered clearly.

The practical heuristic: if a decision comes up in a planning session or architecture discussion, consider whether it warrants an ADR before the meeting ends. The cost of writing one at that moment is low. The cost of reconstructing the reasoning later is high.
