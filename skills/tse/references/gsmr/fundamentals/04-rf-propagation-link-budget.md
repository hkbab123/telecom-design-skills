# RF Propagation & Link Budget Theory for Rail Corridors

The method behind coverage/link budget calculations in Stage 2/3 — read this when the question is "how do I actually calculate coverage along a rail line."

## Why rail corridor propagation is a distinct problem

Unlike a general-area cellular/PMR deployment, GSM-R coverage is needed along a **linear corridor** — the track — not across an area. This changes the propagation planning problem in specific ways: cells are typically arranged in a chain along the line, coverage prediction is usually done along the track centreline (and a defined lateral margin either side, for trackside working and cab-radio use), and tunnels/cuttings/stations each need their own propagation treatment distinct from open-track prediction.

## Link budget structure (same principle as any radio link)

```
Received signal (dBm) = TX power (dBm)
                       + TX antenna gain (dBi)
                       - TX feeder/combiner loss (dB)
                       - Path loss (dB)
                       + RX antenna gain (dBi)
                       - RX body/vehicle/cab loss, if applicable (dB)
                       - Fade margin (dB)
```
Compare against the terminal's receiver sensitivity (OEM-sourced figure). As with any land-mobile link, check both directions — cab radios often have different antenna/installation characteristics from handheld terminals, so uplink and downlink should both be verified, not just assumed symmetric.

## Propagation models by environment

- **Open track** — Okumura-Hata/COST 231-Hata family models, similar to general cellular planning, adjusted for the specific clutter along the corridor (open terrain vs urban crossing vs cutting).
- **Cuttings and embankments** — the track's vertical profile relative to surrounding terrain significantly affects propagation; a deep cutting can shield or, conversely, waveguide signal along its length — treat as a distinct case from flat open track, not a uniform model.
- **Tunnels** — behave as a waveguide (same principle as in general PMR tunnel propagation), essentially never adequately covered by macro-cell prediction from outside; tunnels need dedicated distributed antenna systems (leaky feeder or discrete in-tunnel antennas) planned as a separate exercise.
- **Stations and yards** — denser structure (platforms, canopies, multiple tracks, yard buildings) needs its own clutter treatment, more similar in kind to the "dense plant" case in general PMR planning than to open-track propagation.

## Coverage target expressed along the corridor

The coverage target (analogous to the general "location probability" concept) is typically expressed as **percentage of track length/route-km with adequate signal**, sometimes combined with a required field-strength or signal-quality threshold specifically for handover-viability (see handover fundamentals file — coverage that's merely "adequate" for a stationary receiver isn't necessarily adequate to support handover at train speed, which needs meaningful overlap between adjacent cells, not just a minimum signal floor).

## Worked example (simplified, illustrative figures only)

- BTS TX power: 43 dBm (20 W)
- TX antenna gain: 15 dBi (a directional antenna aimed along the corridor), feeder/combiner loss: 2 dB → effective ERP ≈ 56 dBm
- Path loss at target cell-edge distance (Hata-family model for the specific terrain): 142 dB
- Cab radio antenna gain: 2 dBi, cab/vehicle body loss: 5 dB
- Fade margin: 6 dB

```
Received signal = 56 - 142 + 2 - 5 - 6 = -95 dBm
```
Compare to the cab radio's sensitivity (e.g. -104 dBm, confirm with OEM): closes with roughly 9 dB spare margin at the target cell-edge distance — the same mechanical method as the general RF link budget, applied with rail-corridor-specific antenna/vehicle-loss terms.

## Why this matters for design decisions

- Coverage prediction should always be run along the actual track geometry (curves, gradients, cuttings, tunnels), not a generic straight-line assumption — corridor shape materially affects both direct propagation and handover cell-boundary placement.
- Tunnels and stations need to be scoped as distinct sub-designs with their own propagation treatment from the outset of Stage 2, not folded into the open-track coverage calculation.
- The coverage target needs a handover-viability qualifier (adequate overlap, not just a minimum signal floor at any single point) precisely because trains move continuously through the coverage area at speed — see the handover fundamentals file for why this is GSM-R's most safety-critical design constraint.

Formal reference: general RF engineering practice (Hata/COST 231 models) applied to a linear rail-corridor geometry, per EIRENE's coverage requirements (FRS/SRS).
