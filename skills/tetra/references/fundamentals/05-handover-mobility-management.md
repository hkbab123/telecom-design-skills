# Handover, Cell Reselection & Mobility Management

How a terminal keeps working as it moves — read this when the question is "how does the network know where a radio is" or "what happens during a handover," not just "decide the site list."

## Registration and location updating

When a terminal powers on, it **registers** with the SwMI, which records which cell (base station) it's currently on. As the terminal moves and detects a stronger neighbouring cell's control channel, it performs a **location update** — re-registering on the new cell during idle periods (not mid-call). This is how the SwMI always knows roughly where to route an incoming call without the terminal transmitting continuously.

## Idle-mode cell reselection

While idle (not on a call), the terminal continuously monitors its serving cell's signal quality and scans for stronger neighbours, based on a **neighbour cell list** broadcast by the serving cell. When a neighbour becomes sufficiently stronger (by a defined hysteresis margin, preventing rapid back-and-forth switching at a cell boundary — "ping-ponging"), the terminal reselects to it and performs a location update.

## Handover during an active call

Unlike idle-mode reselection, a handover during a call must happen **without dropping the call** — the terminal and network coordinate a controlled handoff:
1. Terminal reports serving-cell and neighbour-cell signal quality to the network (or measures per network instruction).
2. Network decides to hand over based on signal degradation on the current cell and a stronger available neighbour.
3. Network instructs the terminal to retune to the new cell's traffic channel; a brief signalling exchange re-establishes the call on the new cell.
4. If this fails (network too slow, no channel available on the target cell), the call may drop — this is why handover-heavy environments (linear rail corridors with a train moving at speed through many small cells) need especially careful cell-boundary planning and adequate channel availability at each site.

## Why simulcast avoids this problem

As covered in the SwMI architecture fundamentals file, a simulcast design gives a terminal one continuous coverage area on a single frequency, so there's no cell boundary to cross and therefore no handover event at all within the simulcast zone — this is the main reason simulcast is attractive for fast-moving, linear coverage (rail corridors) despite its synchronisation complexity.

## Handover speed as a design driver

The maximum speed at which a moving terminal can reliably hand over without dropped calls is bounded by cell size and handover execution time — smaller cells (as speed increases, dwell time in each cell shrinks) need faster, more reliable handover signalling. This is a real constraint for rail applications (trains moving through multiple cells) and is one reason a rail-context TETRA deployment (station/yard/depot, generally low terminal speed) is a much simpler handover problem than a comparable GSM-R deployment (trains at line speed) — TETRA in this skill's rail scope is explicitly non-safety-critical, lower-speed voice, not train-borne safety signalling.

## Why this matters for design decisions

- Cell-boundary placement (part of the coverage philosophy in Stage 2 item 1) should account for realistic terminal speed and dwell time at each boundary, not just static coverage prediction.
- If a rail use case ever involves fast-moving terminals (unusual for TETRA's station/yard/depot scope in this skill, but possible), flag it as needing explicit handover-performance analysis, not just static link-budget coverage.
- Simulcast vs conventional multi-site (SwMI architecture fundamentals file) is often decided specifically to avoid handover risk in linear coverage scenarios.

Formal reference: ETSI EN 300 392-2 (mobility management procedures).
