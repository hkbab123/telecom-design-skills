# Redundancy & Failover Mechanics

How resilience actually works technically — the mechanism behind Stage 2 item 4's redundancy targets, not just the decision to have redundancy.

## Exchange (SwMI core) redundancy

- **Hot-standby** — a duplicate exchange running in parallel, continuously synchronised with the active unit's state (registered terminals, active calls, configuration), ready to take over near-instantly if the active unit fails. The failover mechanism itself (automatic detection of failure + automatic switchover) is an OEM-specific implementation detail — confirm the actual failover time and any call-drop behaviour during switchover with the vendor, don't assume "hot-standby" means zero-impact failover in all cases.
- **N+1 / active-active** — for larger multi-exchange networks, redundancy can be distributed (spare capacity shared across the network) rather than one-to-one duplication — a different resilience model with different cost/complexity trade-offs, more relevant to large distributed networks than a single-exchange deployment.

## Base station site redundancy

- **Power redundancy** — UPS/battery autonomy covering short outages, backup generator for extended outages at sites without reliable grid power (especially remote O&G field sites) — sizing method covered in the power-system fundamentals file.
- **Equipment redundancy** — some base station designs include redundant transmit/receive modules within a single site so a partial hardware failure doesn't take the whole site offline; this is an equipment-level OEM design choice to confirm during equipment selection (Stage 2 item 9), not assumed by default.
- **Coverage overlap as implicit redundancy** — where adjacent site coverage overlaps meaningfully, a single site failure degrades (rather than eliminates) coverage in the overlap zone; this is a coverage-planning side-effect worth considering explicitly rather than relying on site-level redundancy alone everywhere.

## Transmission redundancy

Covered in the backhaul fundamentals file (14) — protected ring/star topology so a single transmission path failure doesn't isolate a site.

## What "availability target" actually measures

A network availability percentage (e.g. "99.9%") is a statement about the combined effect of all these redundancy layers plus underlying equipment reliability (MTBF/MTTR) — it isn't achieved by any single redundancy measure alone. When a technical specification states a numeric availability target (Stage 2 item 15), the detailed design (Stage 3) needs to demonstrate, layer by layer, how the combination of exchange redundancy, site power redundancy, and transmission redundancy actually achieves that number — a qualitative "we have hot-standby" statement isn't sufficient evidence on its own.

## Why this matters for design decisions

- Redundancy is a system property built from several independent layers (core, site power, site equipment, transmission) — Stage 2 item 4 should specify each layer's target explicitly, not just a single blanket "redundant" requirement.
- The stated availability KPI (Stage 2 item 15) should be traceable to the actual redundancy design in Stage 3, especially where the network carries process-safety or emergency-response traffic for O&G.
- Failover behaviour (does a switchover drop active calls? how long does it take?) is genuinely OEM-specific — never assert a failover time without sourcing it from the actual vendor's documentation.

Formal reference: no single TETRA standard covers redundancy architecture — this is general telecom high-availability system design practice, applied to TETRA's specific network elements.
