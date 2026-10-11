# Interfacing Other Subsystems

**Technical basis for Rule 2:** time is not frequency; define the boundary and every interface in an ICD.

## Why it matters

The master clock touches almost every other subsystem. Most disputes arise at the boundaries (who is the time authority, who provides the cable, whose accuracy is being measured). Each interface gets an ICD signed by the counterpart owner.

## Interface table

| Counterpart | What crosses the boundary | Points to settle |
|---|---|---|
| **Transmission** | Frequency/phase (SyncE, PTP telecom profiles) vs time-of-day (NTP/PTP for consumers) | Whether both use the same GNSS/PRTC; who owns PTP in the transport; separation of failure modes; no timing loops through ring protection (`transmission/fundamentals/08`) |
| **SCADA / DCS / ESD** | NTP, PTP, IRIG-B/1PPS to servers, controllers, SOE cards | Required accuracy per layer; SIS independence (one-way feed); time-step behaviour on failover |
| **Signalling / interlocking** | Time for logs and recorders; possibly timeouts | Safety status of time use (Rule 7); responsibilities if any use is safety-related |
| **CCTV** | NTP to cameras and recorders; time overlay | Recorder as time client; reporting sync state; retention evidence value |
| **PAGA** | Announcement scheduling and logs | Log time source; scheduled announcement accuracy requirement |
| **PABX / telephony** | Phone displays and call records | NTP source; time zone and daylight-saving handling |
| **GSM-R / TETRA** | NMS logs and event correlation (radio networks take their own air-interface timing) | Don't confuse radio frame timing with time-of-day; NMS as time client |
| **Passenger information / ticketing** | Time on displays and fare/timetable logic | Same source as platform clocks; zone and daylight-saving rules |
| **Enterprise IT** | Directory services, security tools | Boundary between IT and OT time; no public servers (`14`) |
| **Power SCADA / protection** | PTP power profile, IRIG-B | Hop count and accuracy per IEC/IEEE 61850-9-3 |

## What every ICD should state

1. Protocol, profile and version; physical interface and connector.
2. Required accuracy **at the consumer**, with the measurement method.
3. Who owns each side, cable and power.
4. Time policy (UTC vs local, daylight saving, leap-second handling).
5. Behaviour on loss of the master, step limit, and how recovery is handled.
6. Alarm and status exchange.
7. Cybersecurity requirements (authentication, port roles).
8. Test and acceptance method.

## Common mistakes

- Treating "time sync" as one interface, rather than a time-of-day interface and a separate transport frequency interface.
- Letting each counterpart choose its own time source.
- Failing to agree who maintains the cabling between the master and a consumer.
- Missing the SIS independence issue when feeding time to safety systems.
