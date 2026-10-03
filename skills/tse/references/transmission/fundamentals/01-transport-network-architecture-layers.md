# Transport Network Architecture and Layers

**Why this matters:** most transmission design mistakes come from mixing layers: protecting at one layer while the failure sits in another, or buying capacity at one layer when the bottleneck is another. Know the layers before choosing technology.

## The layers (bottom to top)

1. **Physical (fibre and cable)** — glass, cable, ducts, joints, ODFs. Failures here (cuts, water ingress, rodent damage) are the most common and the slowest to repair.
2. **Optical layer** — wavelengths and optical amplification (CWDM/DWDM, ROADMs). Absent in simple single-wavelength designs.
3. **Digital transport layer** — SDH/NG-SDH virtual containers or OTN ODU containers; gives fixed-bandwidth, low-latency, deterministic pipes with strong OAM and fast protection.
4. **Packet transport layer** — Carrier Ethernet or MPLS-TP; statistical multiplexing, flexible bandwidth, Ethernet-native services.
5. **Service layer** — the actual subsystem traffic: E1 circuits (circuit-emulated or native), VLAN-based Ethernet services, serial tails.

A design may use only some layers (a small plant may be fibre plus a Layer-2 packet ring; a long national backbone adds DWDM/OTN).

## Network roles

- **Access** — station/site/field-device attachment; small nodes, low rates (e.g. 1 GbE uplinks).
- **Aggregation/ring** — station or plant rings collecting access nodes; typical rates from STM-4/STM-16 or 1–10 GbE.
- **Core/backbone** — control-centre connectivity and long spans between rings or between plants; highest rates, DWDM/OTN where capacity and reach demand it.

## Where other subsystems plug in

| Subsystem | Typical attachment |
|---|---|
| GSM-R / TETRA backhaul | E1 (TDM) or IP/Ethernet, with strict sync and latency needs |
| SCADA | Ethernet (VLAN) or serial tails, high availability, low bandwidth |
| CCTV | Ethernet, bandwidth-heavy, loss-sensitive |
| PAGA | Ethernet or TDM audio channels, low bandwidth but safety-relevant |
| PABX | E1 trunks or SIP over Ethernet |

## Common mistakes

- Treating the physical layer as "just cable" and letting civil works decide diversity (see `07`).
- Choosing packet-only technology while an unresolved legacy E1 interface exists (see `04`, `05`).
- Sizing only for aggregate bandwidth without per-service class isolation (see `09`).
