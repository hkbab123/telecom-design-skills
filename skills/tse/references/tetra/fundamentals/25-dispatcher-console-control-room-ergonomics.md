# Dispatcher Console & Control Room Ergonomics

The human-operator layer behind the dispatcher subsystem (SwMI fundamentals file, 02, and interfacing fundamentals file, 20) — read this when the question is "how many consoles do we actually need, and what happens if the control room itself is lost," not just "what functions does a console have."

## Sizing the number of concurrent dispatcher positions

The dispatcher console count is a genuine operational-dimensioning exercise, not a default assumption, driven by: the number of distinct talkgroups/operational domains needing simultaneous independent oversight (a large network may need one dispatcher watching rail-corridor operations and a separate one watching station/yard operations, rather than one person monitoring everything), the client's own shift-staffing model for the control room, and a margin for concurrent incident handling (a single incident escalating to "all hands" shouldn't be constrained by having fewer consoles than the response actually needs). This is fundamentally an operational-requirements question the client's own operations function needs to answer — the technical design provides the console hardware/software and the SwMI capacity to support however many positions are specified, but the actual count comes from the client's staffing and operational-concept decisions, not from a TETRA-technical default.

## GIS integration for real-time location visualisation

Where GPS-equipped terminals report location (data-services fundamentals file, 08), a dispatcher wants that plotted on a map, not read as raw coordinates — requiring **GIS (Geographic Information System) integration**: the dispatcher console platform feeding live terminal-location data into a mapping application, either the OEM's own built-in mapping capability or, more often for a client with an existing GIS platform, an integration via that GIS platform's own API consuming the location feed the TETRA dispatcher system exposes. As with the VRS integration point (interfacing fundamentals file, 20), what exactly the OEM's dispatcher platform exposes for this (a standard feed format, a proprietary API, or no native support at all requiring a custom integration) is genuinely OEM-specific and should be confirmed during vendor evaluation rather than assumed available.

## Control room resilience — Disaster Recovery (DR) failover

A **single, un-backed-up control room is a single point of failure for the entire operation's command-and-control function**, independent of how resilient the underlying TETRA network itself is (redundancy fundamentals file, 15) — a fire, evacuation, or other event affecting the primary Central Control Room (CCR) shouldn't leave the network technically operational but with nobody able to dispatch. The standard mitigation is a **Disaster Recovery (DR) control room** — a geographically separate facility with its own dispatcher console positions, kept ready to take over primary control-room function. Design questions worth making explicit rather than assumed:
- **Failover time** — how quickly can the DR room actually take over (near-instant if consoles there are already live and synchronised with the primary room's state, versus a longer manual activation process) — a genuine design parameter to specify, not left implicit.
- **State synchronisation** — does the DR room's console infrastructure maintain live awareness of ongoing calls/incidents (so an operator moving to DR isn't starting from zero context), or is it a cold-standby facility requiring a fuller handover process — an SwMI/dispatcher-platform architecture question, not just a facilities question.
- **Staffing** — whether the DR room is permanently staffed, or staffed only on activation (with the associated activation-time cost) — an operational decision, but one the technical failover-time design should be built around.

## Why this matters for design decisions

- Dispatcher position count should be captured as an explicit operational-requirements input during Stage 1/2 intake (client's shift model, talkgroup/domain split, incident-concurrency margin), not defaulted to a round number.
- GIS integration capability is OEM-specific and should be confirmed during vendor evaluation whenever real-time location visualisation is a stated requirement, mirroring the same caution given for VRS integration.
- DR control room requirements (failover time target, state-synchronisation approach, staffing model) deserve their own explicit line in the technical specification and Stage 3 design — a control-room single point of failure is as real a resilience gap as an un-redundant exchange, and should be scrutinised with the same rigor as the redundancy fundamentals file's network-level requirements.

Formal reference: no TETRA-standard governs control-room/dispatcher-platform design specifically — this is general mission-critical control-room operational practice, applied to the TETRA dispatcher platform's actual capabilities, which are OEM-specific throughout.
