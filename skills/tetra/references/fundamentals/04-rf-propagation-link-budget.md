# RF Propagation & Link Budget Theory

The method behind Stage 2 item 8 and Stage 3 item 7 — read this when the question is "how do I actually calculate coverage/link budget."

## What a link budget is

A running total of every gain and loss between transmitter and receiver, checked against the receiver's sensitivity threshold with margin. If the total received signal is above threshold plus margin, the link closes (coverage exists); if not, it doesn't.

**Simplified link budget structure (downlink example — base station to handheld):**
```
Received signal (dBm) = TX power (dBm)
                       + TX antenna gain (dBi)
                       - TX feeder/combiner loss (dB)
                       - Path loss (dB)
                       + RX antenna gain (dBi)
                       - RX body/vehicle loss, if applicable (dB)
                       - Fade margin (dB)
```
Compare the result to the receiver sensitivity (a fixed spec of the terminal, typically in the range of -103 to -112 dBm for TETRA handhelds — confirm the actual figure against the specific OEM datasheet, never assume). If received signal ≥ sensitivity, the link closes at that point.

## Uplink/downlink balance

TETRA links are usually **uplink-limited**: a handheld's transmit power (commonly around 1–3 W depending on power class) is much lower than a base station's (often tens of watts), so the handheld-to-base-station direction fails before the base-station-to-handheld direction does. This is why link budget calculations should always check uplink, not just downlink — a coverage prediction based only on downlink will overstate real coverage.

## Path loss models

Path loss is the largest and most environment-dependent term. Different models suit different environments — using the wrong one is the single most common source of a coverage prediction that doesn't match reality:

- **Free-space path loss** — the theoretical minimum, used only as a baseline/sanity check, essentially never as the actual design model (real environments always have more loss than free space).
- **Okumura-Hata / COST 231-Hata** — empirical models for outdoor macro-cell coverage in urban/suburban/open terrain, widely used for rail corridor and open-yard coverage prediction.
- **Plant/industrial clutter models** — dense O&G process plant (pipe racks, vessels, structural steel) attenuates and multipaths far more than open terrain or typical urban clutter; generic Hata-family models under-predict loss here. Where possible use a site-specific or plant-specific propagation model, or apply a clutter-loss correction factor derived from a site walk survey — never apply an open-terrain model unmodified to a dense plant environment.
- **In-building/in-structure penetration** — an additional fixed loss allowance (varies hugely by construction: steel-clad industrial buildings attenuate far more than typical office construction) added on top of the outdoor path loss model to predict indoor/in-structure coverage.
- **Tunnel propagation** — behaves like a waveguide, not open-space path loss at all; tunnels typically need distributed antenna systems (leaky feeder or discrete antennas) rather than macro-cell coverage prediction, and are usually treated as a separate design exercise from the general link budget.

## DAQ — the actual quality target a link budget is aiming at

**Delivered Audio Quality (DAQ)** is TETRA's standard subjective voice-quality scale (DAQ 1 = unusable, DAQ 5 = perfect), and **DAQ 3.4** is the conventional minimum acceptable target for critical operational voice — "understandable with slight to moderate effort, no repetition required." A link budget's job is to guarantee this quality, not just "some signal": the received-signal-to-sensitivity margin calculated above needs to be large enough that the resulting bit error rate keeps voice quality at or above the client's stated DAQ target throughout the coverage area, not just above the raw sensitivity floor. In practice this means specifying the location-probability/fade-margin target (below) in terms of the DAQ level it's meant to guarantee, and stating that target explicitly for each criticality tier of area (e.g. DAQ 3.4 minimum for tunnels/control-critical zones, a lower tier acceptable for open yard/non-critical areas) rather than applying one blanket target project-wide.

## In-building and confined-space coverage — DAS, leaky feeder, and BDAs

Standard macro-cell link budget prediction (above) breaks down inside confined or heavily shielded spaces — passenger carriages, plant pump stations, control rooms with steel cladding — where in-building penetration loss is too high or too variable to predict reliably from the outdoor link budget alone. Three technique families address this, each suited to a different confined-space geometry:
- **Distributed Antenna System (DAS)** — a network of low-power antennas distributed through the space, fed from a shared source (often via fibre or coax), giving even coverage through a large or multi-room structure (a large industrial building, a station concourse) rather than relying on one antenna to penetrate from outside.
- **Leaky feeder** — a coaxial cable with intentional gaps in its shielding that radiates and receives along its entire length, the standard solution for long, narrow, RF-hostile spaces (tunnels, as noted above; also long conveyor galleries or narrow plant pipe-racks) where discrete antennas would need impractically dense spacing.
- **Bi-directional amplifier (BDA)** — a repeater that receives the outdoor macro signal, amplifies it, and re-radiates it indoors (and the reverse for uplink) — the simplest and cheapest option for a single confined space (a passenger carriage, a small equipment room) where running a dedicated DAS or leaky feeder isn't justified, but which inherits and amplifies whatever noise/interference is present on the donor signal, so it's a poor choice where the outdoor signal itself is marginal.

Choice among the three is driven by the space's geometry (long-and-narrow → leaky feeder; large-and-open → DAS; small-and-isolated → BDA) and by whether the confined space needs independent capacity (DAS and leaky feeder can be fed by a dedicated site/sector; a BDA simply repeats the donor cell's existing capacity, so a BDA-fed carriage competes for capacity with whatever outdoor cell it's repeating).

## Fade margin

An extra safety margin (dB) added to account for signal variability not captured by the mean path-loss prediction — multipath fading, shadowing, seasonal foliage changes, etc. A typical target is expressed as a **location probability** (e.g. "95% of locations within the coverage area should receive adequate signal"), which converts to a specific fade margin via a log-normal shadowing standard deviation assumption. Never state a fade margin figure without tying it to the location-probability target the client actually requires.

## Worked example (simplified, illustrative figures only)

- Base station TX power: 40 dBm (10 W)
- TX antenna gain: 12 dBi, feeder/combiner loss: 3 dB → effective ERP = 49 dBm
- Path loss at target distance (per chosen model): 135 dB
- Handheld antenna gain: 0 dBi, body loss: 3 dB
- Fade margin: 8 dB

```
Received signal = 49 - 135 + 0 - 3 - 8 = -97 dBm
```
Compare to handheld sensitivity (e.g. -106 dBm, confirm with OEM): -97 dBm is well above threshold, link closes with ~9 dB spare margin at that distance. This is the mechanical method the Stage 2/3 link-budget items are asking for — every figure here is illustrative and must be replaced with the actual project's equipment specs and chosen propagation model.

## Why this matters for design decisions

- The propagation model choice is the single biggest source of prediction error — always match the model to the actual environment (open terrain vs urban vs dense plant vs tunnel), never apply one model uniformly across a mixed-environment site.
- Uplink-limited design means handheld TX power (not base station TX power) is usually the true coverage-limiting factor — check it explicitly, don't assume downlink coverage implies uplink coverage.
- The location-probability target is a client requirement to confirm, exactly like the Erlang grade-of-service target — never assume a "standard" fade margin.

Formal reference: general RF engineering practice (Hata/COST 231 models, ITU-R propagation recommendations) — not TETRA-specific standards, but the accepted method for planning any land-mobile radio system including TETRA.
