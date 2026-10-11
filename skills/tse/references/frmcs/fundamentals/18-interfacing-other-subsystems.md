# Interfacing Other Subsystems

## Why it matters

FRMCS sits between the railway's operations, signalling, control and security systems and the trains. Most project disputes occur at these interfaces: who defines the KPI, who handles errors, who provides what. Each interface needs an ICD signed by the counterpart owner.

## Interface table

| Counterpart | What crosses the boundary | Points to settle |
|---|---|---|
| **Signalling (ETCS, ATO, interlocking)** | Train-control data path, QoS class, fault reporting | Responsibility split and error handling (`12`); evidence for the safety case; behaviour at bearer switch |
| **Dispatcher / control centre** | Voice consoles, group management, recording, alarms | Console integration, identity and group model, priority, recording and retention |
| **Transmission** | Backhaul capacity, latency, protection, QoS | Service-class definition, physical diversity, synchronisation distribution (`14`; the `transmission` subsystem) |
| **Master clock** | Time-of-day for logs, probes, call records | NTP/PTP source for core and OSS; clock accuracy for latency measurement (the `master-clock` subsystem); separate from radio phase sync |
| **SCADA / power** | Site alarms and power status; power supply to sites | Alarm mapping, supply responsibilities |
| **CCTV** | On-board video upload, station video | Bandwidth and policy (`07`); recorder time sync; cybersecurity |
| **Passenger information / ticketing** | Train location and status, passenger-facing data | Application class and bearer (`11`); priority |
| **PAGA** | Station announcements from the control centre | Whether any path rides FRMCS; priority |
| **Legacy radio (GSM-R, TETRA)** | Interworking for voice/groups; migration | Interworking function, identity mapping (`13`) |
| **Public networks and other railways** | Roaming, interconnect, fallback | Agreements, security boundary, QoS (`10`) |
| **Rolling stock** | On-board gateway, antennas, power, train network | Installation, approval, software updates |

## What every ICD should state

1. Interface type, protocol, versions, and the standards baseline.
2. Application KPIs required at the interface and the measurement method.
3. Ownership of each side, equipment, cabling and power.
4. Fault and degradation reporting, and behaviour on loss.
5. Cybersecurity requirements (authentication, zones, logging).
6. Test and acceptance method.
7. Change-control process when either baseline moves.

## Common mistakes

- Treating the signalling interface as a pure data link with no error-handling agreement.
- Not agreeing time sources, so latency measurements are unreliable.
- Several ICDs each define different priorities for the same flow.
- Leaving on-board interfaces to the rolling-stock supplier without a joint specification.
