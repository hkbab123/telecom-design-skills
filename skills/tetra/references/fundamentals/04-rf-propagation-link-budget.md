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

## Outdoor coverage-gap fillers: passive repeaters vs active repeaters/cell extenders

A BDA (above) solves a confined-space coverage problem; a different pair of techniques addresses an **outdoor** coverage gap in trunked mode (TMO) — a valley, a building's radio shadow, a far corner of a large site — without deploying a full additional base station:
- **Passive repeater** — no power, no active electronics: a directional (typically Yagi) donor antenna aimed back at the serving base station, connected by cable directly to a second antenna (often omnidirectional or a corner reflector) that re-radiates the same signal into the shadowed area. Works purely by relaying the donor signal's existing strength into a location the donor antenna itself can't reach line-of-sight — cheap and simple, but only useful where the donor signal reaching the passive repeater's input is already reasonably strong, since a passive repeater has no ability to amplify a weak donor signal, only to redirect it.
- **Active repeater / cell extender** — the same donor-and-shadow-area antenna arrangement, but with active amplification (and often filtering) in between, extending coverage further than a passive repeater can reach and compensating for a weaker donor signal — at higher cost and complexity than a passive repeater, and, like a BDA, it amplifies donor-signal noise/interference along with the wanted signal.

Both are a TMO-level, RF-relay concept — distinct from a **DMO repeater** (fundamentals file 11), which extends direct-mode range between terminals with no base station involved at all, and distinct from a **BDA** (above), which specifically solves confined/indoor coverage rather than an outdoor line-of-sight shadow. Choosing between "add a passive/active repeater" and "add a full base station" is a genuine Stage 2/3 coverage-design decision: a repeater is cheaper and faster to deploy but adds no new trunked capacity (it only extends the donor cell's existing capacity into a new area, the same capacity-sharing caveat as a BDA above) — where the shadowed area also needs meaningful traffic capacity of its own, a full base station is the correct answer, not a repeater.

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
- Before specifying a full additional base station to close a coverage gap, check whether a passive or active repeater actually solves it more cheaply — but only where the gap area doesn't also need dedicated trunked capacity of its own.

Formal reference: general RF engineering practice (Hata/COST 231 models, ITU-R propagation recommendations) — not TETRA-specific standards, but the accepted method for planning any land-mobile radio system including TETRA.
