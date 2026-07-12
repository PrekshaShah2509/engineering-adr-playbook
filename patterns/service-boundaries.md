# Service Boundaries

A system is growing, and the question is whether to keep it as one deployable unit or split it into services, and if so, where the lines go. The boundaries chosen here decide where the system is easy to change and where it is expensive.

## The forces

- Independence versus coordination. Separate services can deploy and scale on their own. They also introduce a network, a contract, and coordination cost at every boundary.
- Team shape. Boundaries that follow how teams actually own work reduce friction. Boundaries drawn against the grain of ownership create a handoff on every change.
- Coupling. A boundary drawn through things that change together turns ordinary changes into cross-service projects. A boundary drawn around things that change independently lets each side move on its own.
- Operational cost. Every service is another thing to deploy, monitor, secure, and keep alive. Splitting too early spends that cost before the independence is needed.

## Common options

- Keep it together. A single deployable unit. Right early, when the domain is still shifting, the team is small, and the coordination cost of splitting outweighs the benefit.
- Split by capability. Separate services around parts of the system that change independently and are owned by different teams. Right when a part has a clear boundary, its own rate of change, and an owner.
- Extract under pressure. Pull out the one part that genuinely needs to scale, deploy, or fail independently, and leave the rest together, rather than splitting everything at once.

## What to capture in the ADR

- Which parts of the system actually change together, and which change independently.
- How the boundary maps onto team ownership.
- The coupling the boundary introduces, and the coordination it removes or adds.
- The operational cost of each new service, and whether the independence is needed now.

## Signals to revisit

- Ordinary changes routinely require several services to coordinate, which points to a boundary in the wrong place.
- A part of the system needs to scale or deploy on a schedule the rest cannot support.
- Team ownership shifts enough that the current boundaries no longer match who owns what.
