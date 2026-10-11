# Mobility and Handover at High Speed

## Why it matters

Every cell boundary is a handover, and trains cross them in seconds. A handover that is slow or fails drops the connection carrying train-control data. Handover performance is a design target to be specified and measured, not a feature to assume.

## Mechanics (conceptual)

- The terminal measures neighbouring cells and reports; the network decides and executes the handover.
- 5G NR and LTE handovers are typically break-before-make with an interruption of tens of milliseconds in good conditions; enhanced mobility procedures (for example, make-before-break or dual-connectivity approaches) reduce interruption. Which are available and mature depends on the release and the vendor; confirm in the baseline and with the OEM.
- **Time to trigger and hysteresis** settings balance early handover (more ping-pong) against late handover (dropped connection). At speed they must be tuned for the cell geometry.

## Time budget worked example

A train at 300 km/h travels 83.3 m/s. If the overlap between cells is 400 m, the train spends 400 ÷ 83.3 ≈ 4.8 s in the overlap. If measurement, reporting and execution need 1.5 s with margin, the overlap is adequate; if the same sequence needed 6 s, it would not be. The overlap length (set by site spacing and antenna patterns) must exceed speed × total handover time with safety margin.

## Design points

1. **Overlap planning** — sector layout, antenna tilt and cell overlap along the corridor; avoid long stretches with a single weak cell.
2. **Neighbour relations and parameter planning** — explicit planning for linear corridors; automated neighbour functions can help but must be controlled.
3. **Interruption-time requirement** — from the application KPIs (`02`), especially train-control data. The specification should state the metric and the measurement method.
4. **Boundary cases** — tunnel portals, station throats, depot entries, network boundaries between railway networks (cross-border), and transitions between railway network and public-network support.
5. **Speed envelope** — the maximum design speed; numerology and Doppler checks (`04`).
6. **On-board behaviour** — dual-radio or multi-link on-board designs can hold a link while the other hands over (`11`).

## Verification

Handover performance is checked by drive/ride testing at line speed and by on-board logging over many runs (`19`), reporting statistics (percentiles), not a single run.

## Common mistakes

- Specifying a handover time without a measurement method.
- Overlap lengths that ignore speed.
- No plan for boundary cases at network edges.
- Treating one successful test run as proof.
