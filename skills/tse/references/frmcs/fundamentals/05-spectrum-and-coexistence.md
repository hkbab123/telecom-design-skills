# Spectrum and Coexistence

**Technical basis for Rule 5:** the frequency position changes the radio design.

## Why it matters

Spectrum decides coverage, capacity, interference exposure and what can legally be built. It is also the least controllable input: allocations are set by regulators, and rules differ by region and change over time.

## Typical European picture (verify against current regulation)

- A harmonised railway band around 1.9 GHz (a 10 MHz TDD allocation) has been designated in CEPT/EU decisions for FRMCS.
- A pair of narrowband blocks in the 900 MHz range, shared with the legacy railway radio band, is available for early FRMCS use and for coexistence with the existing network.
- Regulators in other regions designate different bands, and some countries have national arrangements. Always confirm the national position; this file is a pointer, not the allocation.

## Why the band matters

- **Lower band (900 MHz range):** better propagation, fewer sites, narrow bandwidth, adjacency to the legacy railway radio band and public mobile services.
- **Higher band (1.9 GHz range):** wider bandwidth, higher capacity, shorter range, TDD synchronisation required (`06`, `14`).

## Coexistence issues

- **Legacy railway radio** next to the new carriers: guard bands, filters, carrier placement and site co-location effects (intermodulation, blocking).
- **Adjacent services:** for example cordless telephony or public mobile TDD/FDD systems near the 1.9 GHz range; check spectrum emission masks and adjacent-channel limits.
- **Cross-border:** neighbouring administrations' use of the same band; coordination agreements near borders.
- **Public networks:** where the railway shares sites or runs hybrid delivery, interference between the railway carrier and the public network.
- **Other railway systems:** train-borne radars, wireless links, and co-sited radios; run an interference study.

## Design decisions

1. Which band and bandwidth are available, to whom, and with what licence conditions (Q1d).
2. Carrier configuration, guard bands and filter requirements.
3. Interference study scope and the measurement campaign (spectrum survey before design).
4. Cross-border coordination and who leads it.

## Worked check: co-sited transmitters

When several transmitters share a mast, intermodulation products can land in a receive band. The check is: list all transmit frequencies at the site, compute third-order products (2f1−f2, 2f2−f1), and see whether any fall in a receive band. A spectrum analysis or the OEM's coexistence guidance is required; this arithmetic only flags candidates.

## Common mistakes

- Designing before the spectrum position is confirmed.
- Ignoring the adjacent-band neighbour that already exists.
- Assuming a band is available nationally because it is harmonised regionally.
