# Coverage, Link Budget and Site Planning

**Technical basis for Rule 5:** a higher-frequency carrier needs more sites.

## Why it matters

Site count drives cost, power, civil works and the programme. A designer who assumes existing legacy sites carry over will under-build, and the gap appears only when drive-testing starts.

## Link budget structure

Received level = transmit power + transmit antenna gain − path loss − body/penetration loss − fading margin − other losses + receive antenna gain. The uplink and downlink are checked separately; the weaker one sets the cell range. Include:

- Carriage penetration loss for any user inside the train (`04`).
- Fade margin for the required coverage probability (the contract's coverage percentage and location probability).
- Interference margin from neighbouring cells and coexisting systems.
- Feeder, connector and combiner losses at the site.
- Handover overlap length (`08`).

## Worked example: how much does frequency cost in sites?

Free-space path loss rises by 20·log10(f2/f1) when frequency rises.

20·log10(1900/900) = 6.5 dB extra loss.

With a path-loss exponent n = 3.5 (illustrative for a rural corridor), range shrinks by a factor 10^(−6.5 ÷ (10 × 3.5)) ≈ 0.65. So cell range falls by roughly a third, and a linear corridor needs about 1/0.65 ≈ 1.5 times as many sites (illustrative). Higher-gain or beam-forming antennas, higher power, or a different noise figure can recover part of the gap; the real answer comes from a calibrated propagation model.

## Site reuse

- Existing legacy sites are candidates, not a given: check tower loading, mast structure, space, power, backhaul and antenna height for the new band.
- Co-location raises coexistence work (`05`).
- New infill sites may be needed in cuttings, curves, stations, depots and viaducts.

## Special environments

- **Tunnels** — leaky feeder, distributed antenna systems, or radiating cable; check the cable's frequency range and coupling loss, the capacity of a shared medium, and the multi-operator/multi-band combiner design.
- **Underground stations and platforms** — distributed antennas; separation of train-side and passenger-side coverage.
- **Viaducts and cuttings** — shadowing and reflection effects.
- **Depots and yards** — coverage for shunting and maintenance; lower speed.
- **Repeaters and radio heads** — valid for gap-filling but add delay and noise; confirm they are allowed in the baseline.

## Design decisions

1. Coverage requirement per application (not only the critical ones).
2. Propagation model and its calibration measurements.
3. Site-reuse assessment versus new build.
4. Tunnel and station coverage technology.

## Common mistakes

- Using one link budget for uplink and downlink.
- Leaving out body loss.
- Reusing the legacy site spacing for a higher band.
- Treating tunnels as an afterthought.
