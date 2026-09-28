# Redundancy & Failover Mechanics

How resilience actually works technically for a GSM-R network — the mechanism behind redundancy targets in the Stage 2/3 sequences, including the cross-border case, not just the decision to have redundancy.

## Core network redundancy (MSC/BSC/HLR)

- **Hot-standby core elements** — a duplicate MSC (and associated BSC/HLR capacity) running in parallel, synchronised with the active unit's state, ready to take over on failure — same principle as general telecom core redundancy, with the same caveat: actual failover time and call-continuity behaviour during switchover are OEM-specific and should be confirmed with the vendor's documentation, not assumed to be zero-impact.
- **Geographic redundancy** — for larger national networks, core elements may be split across geographically separate sites so a single site-level incident (fire, power loss, physical damage) doesn't take down the entire national core — a more elevated resilience requirement than a typical enterprise telecom deployment, given GSM-R's safety-relevance.

## BTS site redundancy

Power redundancy (UPS/battery, generator — see power-system fundamentals file) is the dominant BTS-level redundancy concern along a rail corridor, particularly for remote sections without reliable grid access. Equipment-level redundancy within a single BTS (redundant transmit/receive modules) is an OEM-specific equipment design choice to confirm during equipment selection, same principle as general telecom practice.

## Transmission redundancy

Covered in the backhaul fundamentals file (14) — protected topology so a single transmission-path failure doesn't isolate a site, with heightened importance wherever ETCS-bearer traffic is involved.

## Cross-border redundancy — the specific mechanics

Beyond redundancy within each country's own core (covered above, applied independently to each national core in the recommended independent-core-per-country architecture), the **interworking interface** between the two countries' cores (network-architecture fundamentals file) needs its own resilience consideration: if the interworking link or interface fails, does cross-border service degrade gracefully (each country's core continues serving its own domestic traffic normally, only cross-border continuity is affected) or does it risk wider disruption? The independent-core architecture's main resilience advantage is precisely that a failure on one side's core, or in the interworking link itself, is contained rather than propagating into the other country's domestic operation — this containment property is the practical payoff of the architecture recommendation in the network-architecture fundamentals file, not just a regulatory/ownership tidiness argument.

## What an availability target actually measures

As in general telecom practice, a stated network availability percentage is the combined result of every redundancy layer (core, BTS, transmission) plus underlying equipment MTBF/MTTR — Stage 3's detailed design needs to demonstrate, layer by layer, how the design achieves a stated target, especially wherever the network carries ETCS-bearer or other safety-relevant traffic, where a qualitative "redundancy is implemented" statement isn't sufficient evidence for the safety case (see the functional-safety fundamentals file).

## Why this matters for design decisions

- Redundancy should be specified per layer (core, BTS power, transmission, and — for cross-border — the interworking interface specifically) rather than as one blanket "redundant network" requirement.
- The cross-border architecture's failure-containment property is worth stating explicitly as the technical justification when presenting the independent-core-per-country recommendation to a client or reviewer, not just citing it as a regulatory-alignment preference.
- Wherever ETCS-bearer traffic is in scope, redundancy design should trace to a documented safety-case argument (functional-safety fundamentals file), not just a general high-availability design philosophy.

Formal reference: no single EIRENE clause covers redundancy architecture comprehensively — general telecom high-availability practice, applied to GSM-R's specific network elements and EIRENE's availability requirements.
