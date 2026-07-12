# Synchronous vs Asynchronous

Two components need to communicate. The question is whether the caller waits for a response or hands off the work and moves on. The choice shapes coupling, failure behavior, and how the system degrades under load.

## The forces

- Immediacy versus decoupling. Synchronous calls give an immediate answer and simple reasoning. Asynchronous messaging decouples the two sides so one can be slow or down without blocking the other.
- Simplicity versus resilience. A synchronous call is easy to write and easy to trace. An asynchronous flow is more resilient under load but harder to follow and to debug.
- Consistency versus availability. Waiting for a response keeps state consistent across the call. Handing off means the two sides are briefly out of step by design.
- Failure blast radius. A synchronous dependency chain tends to fail together. An asynchronous boundary contains failure to one side and lets the other catch up later.

## Common options

- Synchronous request-response. The caller waits. Right when the result is needed to continue, the operation is fast and reliable, and the two sides are naturally coupled.
- Asynchronous messaging or events. The caller hands off work to a queue or an event stream. Right when the work can happen later, when the sides should scale and fail independently, or when several consumers care about the same event.
- Synchronous with a fallback. Call synchronously, but degrade to a queued or cached path when the dependency is slow or unavailable, so a slow dependency does not take the caller down with it.

## What to capture in the ADR

- Whether the result is needed to continue, or can be handled later.
- How the two sides should behave when the other is slow or down.
- The consistency the flow needs, and where a brief gap is acceptable.
- The added operational cost of a queue or event system, if one is introduced.

## Signals to revisit

- A synchronous dependency becomes a recurring source of cascading failures.
- The coupling between the two sides makes independent deploys difficult.
- Volume grows to where the caller cannot afford to wait.
