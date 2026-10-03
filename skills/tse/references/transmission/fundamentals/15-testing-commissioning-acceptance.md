# Testing, Commissioning and Acceptance

**Why this matters:** every design claim (loss budget, diversity, switch time, sync) is only true once measured.

## Fibre acceptance (physical layer)

- **OTDR** — trace each fibre, bidirectionally where possible; checks length, event locations, splice and connector loss, anomalies.
- **Insertion-loss test** with a light source and power meter — the reference measurement for total span loss (IEC 61280 procedures).
- **Connector inspection** — end-face cleanliness and quality inspection before mating (IEC 61300 series).
- Compare results to the link-budget sheet; records form part of the as-built package.
- For re-used or leased fibre, test before reliance; do not accept stated figures.

## Equipment FAT

Factory test of the delivered configuration: node functions, protection-switch time, sync behaviour (reference loss, holdover, SSM), service mapping, NMS alarms.

## System SAT

- **End-to-end service activation** — Ethernet services against bandwidth profile, delay, loss and jitter (ITU-T Y.1564; RFC 2544 for throughput-style tests).
- **BER testing** for TDM/OTN services over a defined soak period.
- **Protection tests** — pull or disconnect each protected path in turn and measure switch time and service impact; where practical simulate a **physical** break at a field location (see Rule 1).
- **Sync verification** — measure frequency accuracy/wander at nodes; test reference loss and recovery.
- **NMS integration** — alarms reach the control room, and clear correctly.
- **Interface tests** — each ICD verified with the counterpart subsystem (see `16`).

## Diversity verification on site

Walk or inspect each protected path pair; confirm that the as-built routes match the SRLG register. Surprising shared structures commonly appear during installation.

## Acceptance records

Test certificates, OTDR traces, measurement tables, SRLG register as-built, configuration backups, and a punch list with closure dates.

## Common mistakes

- Accepting vendor FAT as a substitute for site protection tests.
- Testing protection by disabling a port only, without checking an actual optical break.
- Archiving OTDR results without the trace files, losing the baseline for future fault location.
