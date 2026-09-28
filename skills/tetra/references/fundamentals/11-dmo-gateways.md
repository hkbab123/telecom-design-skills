# DMO & Gateways

The mechanics behind Stage 2 item 10 — read this when the question is "how does Direct Mode actually work," not just "decide whether it's needed."

## DMO at the protocol level

As introduced in the air-interface fundamentals file, DMO bypasses the SwMI entirely: terminals communicate directly on a shared DMO channel using a simplified point-to-multipoint scheme, with no trunking, no handover, and no central call management. Coverage is limited to direct radio-to-radio range — typically far less than TMO's base-station-assisted coverage, and highly dependent on terrain/obstruction between the terminals (line-of-sight or near-line-of-sight generally needed for reliable DMO).

## Why DMO is used

- **Outside trunked coverage** — field/emergency-response teams working beyond the TMO network's coverage footprint (common at the edges of large O&G sites, or in areas not yet built out).
- **Network fallback** — if the trunked network fails (SwMI outage, backhaul loss to a site), DMO-capable terminals can still communicate directly with each other as a degraded-mode fallback, which is often a specific requirement for O&G emergency-response fleets.
- **Simpler tactical grouping** — a small team working a task in close proximity can use DMO without needing to be registered on or route through the main network at all.

## DMO repeater

A **DMO repeater** extends DMO's limited direct range by receiving on one DMO channel and retransmitting on the same or a paired channel, without involving the SwMI — still direct-mode from the terminals' perspective, but with extended coverage. Distinct from a gateway (below): a repeater only extends DMO range, it doesn't bridge DMO to the trunked network.

## DMO/TMO gateway

A **gateway** is a fixed or vehicle-mounted device that bridges a DMO channel to the TMO trunked network — a DMO terminal communicating through a gateway effectively reaches TMO users (and vice versa) as if it were part of the trunked network, even though its own radio link is still direct-mode. This is the mechanism that answers "can a DMO field team talk to the control room via the trunked network" — without a gateway, a DMO group is isolated from TMO users entirely.

## Why this matters for design decisions

- If the client's operational concept includes "field team must be able to reach the control room" while also using DMO in coverage gaps, a gateway (not just a repeater) is the actual requirement — this distinction is easy to miss and worth confirming explicitly during Stage 2 item 10.
- DMO repeater/gateway placement is itself a coverage-planning exercise (similar in kind to base station siting, but for direct-mode range), which should be scoped alongside the main coverage philosophy (Stage 2 item 1), not treated as an afterthought.
- Network-fallback DMO capability (as a resilience feature, not just a coverage extension) should be an explicit requirement if the client's safety case depends on communication continuing through a SwMI outage — tie it to the reliability/safety-case discussion in Stage 2 item 15.

Formal reference: ETSI EN 300 396 series (Direct Mode Operation).
