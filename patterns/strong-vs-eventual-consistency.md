# Strong vs Eventual Consistency

More than one place holds the same data, or a read follows a write closely enough that freshness matters. The decision is how up to date the data has to be, and the team pays for that freshness in availability and complexity.

## The forces

- Correctness versus availability. Strong consistency guarantees every read sees the latest write. It costs coordination, which costs availability and latency under partition or load.
- User expectation. Some data must be exactly right the instant it is read, like a balance or an inventory count. Some can lag by seconds without anyone noticing, like a view count or a recommendation.
- Where the cost lands. Strong consistency pushes complexity into the infrastructure. Eventual consistency pushes it into the application, which has to handle stale reads and reconcile differences.
- Blast radius of being wrong. The cost of serving stale data ranges from harmless to a serious correctness bug depending on the field.

## Common options

- Strong consistency. A read always reflects the latest write. Right for data where being stale is a correctness problem: money, inventory, access control.
- Eventual consistency. Reads may briefly lag writes, and the system converges. Right for data that tolerates a short delay and where availability and scale matter more than immediate freshness.
- Mixed by field. Hold the parts that must be exact under strong consistency and let the rest be eventual, rather than paying the strongest guarantee across the whole system.

## What to capture in the ADR

- Which data must be exactly right on read, and which can lag.
- The staleness window that is acceptable, stated concretely.
- How the application handles a stale read, and how conflicts reconcile.
- The availability the system needs, and what strong consistency would cost it.

## Signals to revisit

- Stale reads start causing user-visible correctness issues on data that was assumed safe.
- The coordination cost of strong consistency becomes an availability problem.
- The write-to-read pattern shifts enough to change what freshness the system needs.
