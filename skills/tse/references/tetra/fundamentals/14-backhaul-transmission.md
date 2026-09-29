# Backhaul/Transmission Technical Basis

The technical characteristics behind Stage 3 item 11 — read this when the question is "how do I actually choose between fibre, microwave, and leased line," not just "decide the backhaul."

## What backhaul connects

The transmission link between each base station site and the exchange (SwMI core) — carries the aggregated voice/signalling/data traffic from that site back to the network. Every base station needs one; the choice of technology depends on site accessibility, available infrastructure, distance, and required capacity.

## Fibre

Highest capacity, lowest latency, most future-proof — the preferred option wherever fibre infrastructure exists or can be economically laid (common in rail corridors, which often already have fibre for signalling/telecoms; less common at remote/dispersed O&G field sites without existing duct/route infrastructure). Capacity is essentially not a constraint at TETRA's traffic volumes — dimensioning fibre backhaul is rarely the limiting design question once fibre is available at all.

## Microwave (point-to-point radio link)

Used where fibre isn't available or economical — a directional radio link between the site and a hub/exchange location, requiring line-of-sight between the two ends. Capacity is finite (link capacity depends on the specific radio equipment and licensed spectrum used for the microwave hop itself — a separate frequency allocation from the TETRA band) and needs its own link-budget-style planning (path clearance, fade margin — conceptually similar to the RF link budget in fundamentals file 04, but for the microwave hop, not the TETRA air interface). Common for remote O&G sites where fibre isn't practical and a clear line-of-sight path to a hub exists.

## Leased circuit

A transmission service leased from a telecom carrier (could be delivered over the carrier's own fibre, microwave, or other infrastructure) — avoids the capital cost of building dedicated transmission infrastructure, at the cost of ongoing lease fees and dependency on the carrier's own network reliability/SLA. Often used where neither self-built fibre nor a clear microwave path is practical, or where a project timeline doesn't allow for building dedicated infrastructure.

## Dimensioning backhaul capacity

Backhaul bandwidth needs to cover the site's dimensioned voice traffic (from Erlang-based capacity, fundamentals file 03 — each simultaneous voice call has a bit-rate requirement from the codec, fundamentals file 09) plus signalling overhead plus any data service traffic (fundamentals file 08) plus network management traffic. For most TETRA sites this aggregate figure is modest by modern telecom standards — the real design driver is usually availability/redundancy and route diversity, not raw capacity.

## Redundancy at the transmission layer

Ring or star topology with protected paths (see redundancy/failover fundamentals file 15) matters more for transmission than for the TETRA-specific equipment itself — a single fibre cut or microwave hop failure shouldn't take an entire site (or worse, a whole region if sites are daisy-chained) offline. This is the technical detail behind Stage 2 item 4's "ring/star transmission protection between sites."

## Why this matters for design decisions

- Site accessibility (existing fibre route? clear line-of-sight for microwave? carrier presence for a leased circuit?) usually determines the backhaul choice more than raw capacity requirements — survey this early, during Stage 3's detailed site survey (item 3).
- Remote/dispersed O&G field sites are the case most likely to need microwave or leased circuits rather than fibre — plan backhaul technology per-site, not as one blanket decision for the whole network.
- Redundant/protected transmission topology is a resilience decision with real cost implications — confirm the client's actual availability requirement (Stage 2 item 4/15) before defaulting to a fully protected ring everywhere.

Formal reference: general telecom transmission engineering practice — not TETRA-specific.
