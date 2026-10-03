# SDH / NG-SDH Fundamentals

**Why this matters:** many rail and O&G networks still run SDH, and legacy E1-based subsystems depend on it. Even new designs need to interwork with it.

## Hierarchy (ITU-T G.707)

| Level | Rate |
|---|---|
| STM-1 | 155.52 Mbit/s |
| STM-4 | 622.08 Mbit/s |
| STM-16 | 2,488.32 Mbit/s |
| STM-64 | 9,953.28 Mbit/s |

## Containers

E1 (2.048 Mbit/s) is carried in VC-12; larger payloads in VC-3 / VC-4. Higher-order and lower-order paths are cross-connected in add-drop multiplexers (ADM) and digital cross-connects.

## Protection (ITU-T G.841)

- **MSP (multiplex-section protection)** — 1+1 / 1:1 linear or MS-SPRing ring protection at the section level.
- **SNCP (sub-network connection protection)** — path-level 1+1 protection, common in rings.
- Typical switch time target is of the order of tens of milliseconds (illustrative: ≤50 ms); verify the client's requirement.

## NG-SDH (next-generation)

Adds Ethernet-friendly mapping to SDH:
- **GFP (generic framing procedure)** maps Ethernet frames into SDH payloads.
- **VCAT (virtual concatenation)** groups containers to match the required rate efficiently.
- **LCAS (link capacity adjustment scheme)** lets the group grow, shrink or drop a member without hit traffic.

This lets an SDH ring carry Ethernet services (e.g. CCTV, SCADA LAN extensions) while keeping TDM service for legacy needs.

## Strengths and limits

- Strong: deterministic latency, mature OAM, fast protection, clean E1 handoff, strong sync distribution.
- Limits: fixed-bandwidth pipes make bursty IP inefficient; platform and skill base are ageing; new-equipment availability is shrinking.

## When SDH is still the right answer

When a significant legacy E1 base exists and migration is gated by other subsystems' refresh cycles (see Q1b). Otherwise packet transport with circuit emulation is usually the forward path (see `05`).
