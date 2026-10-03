# Synchronisation and Timing

**Technical basis for Rule 5:** timing is part of transport's job.

## Why it matters

TDM-based services (E1 links to radio base stations, legacy PABX trunks) require all equipment to run at the same frequency; otherwise frame slips occur, causing audible clicks, data errors, or alarms. Some services (e.g. certain radio technologies, time-stamped logs, protection relays) need **phase/time** alignment, not just frequency.

## Frequency synchronisation

- **PRC (primary reference clock, ITU-T G.811)** — the traceable source (often GNSS-disciplined or caesium).
- **SSU/BITS (ITU-T G.812)** — synchronisation supply unit that cleans and distributes timing.
- **SEC (ITU-T G.813)** — SDH equipment clock; takes timing from line or external input.
- **Synchronous Ethernet (SyncE, ITU-T G.8261/G.8262)** — frequency carried by the Ethernet physical layer.
- **SSM (synchronisation status messages)** — carry clock quality so nodes choose the best source and avoid timing loops.

## Phase and time synchronisation

- **PTP (IEEE 1588)** with ITU-T telecom profiles (G.8265.1 for frequency, G.8275.1 for phase with on-path support).
- Boundary clocks at every node (full on-path support) give the best phase performance; unaware nodes degrade it.
- GNSS at sites gives time directly but adds vulnerability (jamming, antenna siting, tunnel sections where GNSS is unavailable).

## Design decisions

1. **Reference sources** — at least two independent PRC/PRTC locations in different areas; do not rely on one GNSS receiver.
2. **Distribution tree** — avoid timing loops; define primary and secondary paths per node.
3. **Holdover** — how long a node maintains acceptable timing after losing reference; sized to the longest credible outage.
4. **Tunnels** — GNSS is not available below ground; sync must be distributed over the transport.
5. **Interface with a master clock system** — when a separate master-clock/time subsystem exists, define who is the master and how time is handed over (see `16`).

## Common mistakes

- Closing a timing loop through ring protection switches.
- Single GNSS antenna feeding the entire network.
- Using circuit emulation without a defined recovered-clock source.
