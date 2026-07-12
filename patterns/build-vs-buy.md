# Build vs Buy

A capability is needed, something already exists that provides it, and the team has to decide whether to build its own or adopt what is available. The decision recurs at every layer, from a single library to an entire platform.

## The forces

- Speed now versus control later. Adopting is usually faster to get running. Building gives control over how the capability evolves.
- Core versus supporting. Some capabilities are central to how the product works or how the team needs to grow. Others are undifferentiated and better handed to someone whose whole job is to run them well.
- Cost that is visible versus cost that accumulates. A vendor has a price. A dependency also has an integration surface, a switching cost, and a limit on what the team learns by not building it.
- Expertise. Building develops expertise in a domain. Adopting develops expertise in operating someone else's system.

## Common options

- Adopt. Use a vendor service, a managed offering, or an open-source library. Right when the capability is not differentiated and the cost of ownership would be significant relative to the value of building it.
- Build. Own the capability. Right when it shapes how the product works in ways that matter, when the problem is specific enough that adopted solutions need heavy customization, or when the team needs the expertise to execute its roadmap.
- Wrap and defer. Adopt now behind an interface the team controls, so the decision can be revisited without rewriting everything that depends on it.

## What to capture in the ADR

- Whether the capability is core or supporting, and why.
- The integration surface: how deeply the choice will be embedded and how many things will depend on it.
- The switching cost: what it would take to move off this in two to three years.
- What the team gives up in expertise by not building it, where that matters.

## Signals to revisit

- The capability drifts from supporting toward core as the product evolves.
- Integration overhead grows faster than the value the adopted solution provides.
- The vendor's direction diverges from what the product needs.
