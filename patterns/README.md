# Decision Patterns

Some architecture decisions recur across teams and systems. The specifics differ, but the forces at play and the options on the table are familiar.

These patterns are not decisions. They are decision landscapes: the forces that tend to pull in different directions, the options teams usually weigh, and what is worth capturing in the ADR when you make the call. Use them as a starting point, not an answer.

Each pattern maps onto the standard ADR structure. The forces inform the Context. The options and their trade-offs inform the Rationale and the Consequences.

## Patterns

- [Build vs buy](build-vs-buy.md) — whether to build a capability or adopt something that exists
- [Synchronous vs asynchronous](synchronous-vs-asynchronous.md) — request-response or messaging between components
- [Strong vs eventual consistency](strong-vs-eventual-consistency.md) — how fresh the data has to be, and where
- [Service boundaries](service-boundaries.md) — whether to split a system into services, and where the lines go
