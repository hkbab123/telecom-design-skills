# Frequency Planning & Interference

The technical basis behind Stage 2 item 5 — read this when the question is "why does the frequency plan matter" or "how does reuse actually work," not just "which band applies."

## Channel raster and duplex spacing

TETRA channels are spaced on a **25 kHz raster** within whatever band the national regulator allocates (commonly somewhere in 380–470 MHz — always confirm the actual allocation, never assume). Base station transmit (downlink) and receive (uplink) are separated by a **duplex spacing** specific to the allocated band plan (varies by regulator/region — confirm per project), so a "channel" in practical terms is really a paired uplink/downlink frequency, not a single frequency.

## Frequency reuse

A multi-site network doesn't need a unique frequency at every site — the same frequency can be reused at sites far enough apart that their signals don't meaningfully interfere with each other. The core planning task is choosing a **reuse pattern** (how many distinct frequency groups, and which sites get which group) that balances two competing pressures:
- **More reuse (fewer distinct frequency groups)** → more spectrum efficiency, but higher risk of co-channel interference between sites using the same frequency.
- **Less reuse (more distinct frequency groups)** → lower interference risk, but requires more total spectrum, which may not be available from the regulator's allocation.

## Co-channel and adjacent-channel interference

- **Co-channel interference** — two sites using the *same* frequency close enough together that their coverage areas overlap with both signals present at comparable strength, degrading or blocking calls in the overlap zone. Managed by reuse distance (physical separation) and/or antenna directionality (sectoring) to reduce the overlap.
- **Adjacent-channel interference** — a receiver picks up energy from a *neighbouring* frequency channel due to imperfect filtering, degrading reception even without a direct co-channel conflict. Managed by guard-band planning and equipment filter specifications (an OEM-sourced figure — confirm with the vendor's RF datasheet).

## Interference from outside the network

Beyond internal reuse planning, coordinate with the national regulator on **adjacent licensed users** sharing the same band (other PMR operators, sometimes broadcast or other radio services near the band edge) — this is a regulatory approval step (Stage 2 item 14) as much as a technical one, since interference coordination is typically brokered through the regulator's licensing process.

## Why this matters for design decisions

- Reuse pattern choice directly trades off against the total spectrum the regulator actually grants — if the allocation is narrow, plan for a smaller number of distinct frequency groups and manage interference more through site geometry/sectoring than through frequency separation.
- Dense multi-site deployments (many O&G sites close together, or many rail stations along a short corridor) are the cases where reuse planning matters most — a single-site deployment can often skip most of this.
- This is a genuinely specialist RF planning task, often done with dedicated planning software (see the testing/commissioning fundamentals file for how predictions get field-verified) — treat the frequency plan as a deliverable requiring RF planning expertise, not something to hand-wave in a generic technical spec.

Formal reference: ETSI EN 300 392 series (band plan/channel raster references) plus the national telecom regulator's specific band-plan and licensing conditions — always project- and country-specific.
