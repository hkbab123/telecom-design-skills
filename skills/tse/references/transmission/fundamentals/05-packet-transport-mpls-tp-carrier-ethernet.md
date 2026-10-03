# Packet Transport: MPLS-TP and Carrier Ethernet

**Why this matters:** most new rail and O&G backbones are packet-based; the design question is how to give packet networks the determinism that operational services expect.

## Carrier Ethernet

Defined by MEF service attributes (MEF 10.x, MEF 6.x):
- **E-Line** — point-to-point (e.g. station to control centre).
- **E-LAN** — multipoint LAN.
- **E-Tree** — rooted multipoint (e.g. many stations to one control centre, with no station-to-station traffic).

Key attributes: bandwidth profile (CIR/EIR), class of service, frame delay, frame delay variation, frame loss.

## Ring and linear protection

- **ERPS (ITU-T G.8032)** — Ethernet ring protection switching; typical sub-50 ms target on small rings (verify with vendor).
- **G.8031** — Ethernet linear protection (1+1 or 1:1).
- Spanning-tree variants (RSTP/MSTP) are slower and less predictable; generally not preferred for backbone use.

## MPLS-TP (ITU-T G.8110.1, G.8131)

A transport-oriented subset of MPLS: connection-oriented label-switched paths with SDH-like OAM and protection, but without the IP control-plane complexity. Offers deterministic path control and in-band OAM; circuit emulation (TDM pseudowire) carries legacy E1 over the packet network.

## OAM

- **Y.1731 / 802.1ag** — Ethernet connectivity fault management and performance monitoring (delay, loss).
- Use OAM at the service level so the control centre can see per-service health, not just link status.

## Circuit emulation (for legacy E1)

TDM pseudowires carry E1 over packet. Requirements: tightly controlled delay variation, and synchronisation (clock recovery) to be designed explicitly (see `08`). Poorly designed emulation is the usual cause of radio-backhaul slips and alarms.

## QoS

Map each subsystem to a class of service (see `09`): safety-relevant control and voice-alarm traffic highest priority with guaranteed bandwidth; CCTV as high-bandwidth but loss-tolerant class; enterprise best-effort.

## Common mistakes

- Using Ethernet ring protection without verifying actual switch time under real load and fault types.
- Giving CCTV and SCADA the same class and letting video bursts starve control traffic.
- Assuming a pseudowire "just works" without a sync plan.
