# Capacity Dimensioning and Service Mapping

**Technical basis for Rule 2:** transport is the shared dependency; design per service class, not just aggregate capacity.

## Build the service matrix first

One row per service, with at least:

| Field | Example |
|---|---|
| Service / owner subsystem | CCTV station cameras → control-centre VMS |
| Endpoints | Station A → OCC |
| Interface | 1 GbE (VLAN) / E1 / serial |
| Bandwidth | Committed and peak |
| Latency / jitter tolerance | e.g. tight for voice and radio backhaul |
| Protection class | 1+1 / ring / none |
| Priority class | Critical / high / best-effort |
| Growth | Expected change over the planning horizon |

## Aggregation

Sum per ring segment and per direction, then add growth margin. Work out the **worst-case segment** (usually the span nearest the control centre) because aggregate load concentrates there.

### Worked example (illustrative)

A ring with 10 stations. Per station: CCTV 20 Mb/s × 8 cameras = 160 Mb/s; SCADA 2 Mb/s; PAGA 2 Mb/s; radio backhaul 4 E1 = 8 Mb/s; enterprise 20 Mb/s. Per-station ≈ 192 Mb/s; ten stations ≈ 1.9 Gb/s toward the control centre. With 50% growth ≈ 2.9 Gb/s, so a 1 GbE ring is inadequate and a 10 GbE (or STM-16 plus separate Ethernet) ring is the minimum. Real figures must come from the subsystem designers.

## Oversubscription

Video and enterprise traffic can be oversubscribed with care; safety-relevant control and alarm services get **guaranteed** bandwidth. Decide the policy explicitly and write it into the spec.

## Behaviour under failure

During a protection event or ring cut the available capacity may halve. Define which services must survive at full rate, which may degrade (e.g. CCTV reduced frame rate), and which may drop. Encode as priority classes and shaping rules.

## Growth

State the planning horizon (e.g. 10 years) and where headroom lives: spare fibre, spare line cards, unused wavelengths. Upgrade paths should not need re-pulling cable.

## Common mistakes

- Sizing from average rather than peak traffic.
- Forgetting that protection traffic consumes capacity.
- Aggregating at the ring level and missing a congested single span.
