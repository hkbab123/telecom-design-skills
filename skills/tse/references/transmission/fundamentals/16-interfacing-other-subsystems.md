# Interfacing with Other Subsystems

**Why this matters:** transport is the common dependency; an unclear interface is the usual source of finger-pointing during commissioning.

## ICD content (per interfacing subsystem)

1. Physical interface: medium, connector, rate, location of handoff (ODF, patch panel, switch port).
2. Service definition: service type (E1, Ethernet VLAN, serial), bandwidth, priority class, protection class.
3. Timing: whether the subsystem needs a timing reference from the transport, and which type/quality.
4. Latency, jitter and availability commitments, and how each is measured.
5. Alarms and management: what faults the transport reports to the subsystem and vice versa.
6. Cybersecurity: segmentation, addressing plan, who owns the boundary device.
7. Responsibility split: who tests, who maintains, who is first contact for a fault.

## Subsystem-specific points

| Subsystem | What to settle |
|---|---|
| **GSM-R** | E1 or IP backhaul between base stations and core; sync source and quality; delay limits; cross-border links if any; see GSM-R `fundamentals` on backhaul |
| **TETRA** | E1/IP between base stations and switching nodes; sync; redundancy aligned with TETRA site-link design |
| **SCADA** | Ethernet or serial extension, deterministic path, redundancy aligned with SCADA ring/PLC redundancy; IT/OT separation |
| **CCTV** | High-bandwidth service class, multicast handling if used, loss tolerance; storage location versus transport capacity |
| **PAGA** | Audio/IP channels with priority; GA path protection consistent with PAGA's safety classification |
| **PABX** | E1 or SIP trunks; sync if TDM |
| **Master clock** | Who is master; how time and frequency enter the transport; GNSS-denied sections |
| **Enterprise IT** | Separation, firewall boundary, shared-fibre agreements |
| **Fibre sensing** | If sharing cable with telecom, agree fibre allocation and optical-power limits |

## Cross-subsystem consistency checks

- Redundancy: if the subsystem has dual-homed equipment, the transport must give each home a genuinely separate path (Rule 1).
- Sync: if two subsystems derive timing from different references, document which wins.
- Capacity: sum of all subsystems' declared needs fits the service matrix (see `09`).

## Common mistakes

- Subsystem designers assuming "the network" is redundant without specifying how.
- No named owner for the handoff demarcation point.
- Late discovery that a subsystem needs E1 or serial that the chosen technology does not provide.
