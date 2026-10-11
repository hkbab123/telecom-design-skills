# Tender Stage — Master Clock / Time Synchronisation

PMC + specialised time-synchronisation Consultant engaged by the client, building the technical specification.

**Draft ordered decision sequence (public-standards-informed draft — needs correction by a practising time-synchronisation engineer):**

1. **Consumer catalogue and accuracy budget** — every subsystem that consumes time (SCADA/DCS, signalling, CCTV, PAGA, PABX, radio NMS, PIS, ticketing, enterprise IT, display clocks), with owner, protocol, required accuracy and criticality class (Rule 1).
2. **Time policy** — UTC vs local time per consumer family, time zone, daylight-saving handling, leap-second handling, date/time format (Rule 6).
3. **Time authority and hierarchy** — primary and secondary master clocks, sub-masters per site or zone, their locations and the source-priority order (Rule 4).
4. **Reference source architecture** — GNSS constellations, receiver count, antenna siting, any terrestrial or fibre-delivered second reference (Rule 3).
5. **Holdover requirement and oscillator class** — sized to the longest credible reference outage against the tightest accuracy budget.
6. **Distribution protocols per consumer family** — NTP, PTP profile, IRIG-B/1PPS, serial time string, impulse line; who provides each and at what accuracy.
7. **Redundancy and failover** — hot-standby behaviour, maximum permitted time step on switchover, resolution when two masters disagree.
8. **Network design for time** — dedicated VLAN/QoS, on-path support requirement for PTP, asymmetry control, interplay with the transport network (Rule 5).
9. **Display clock system** — types, quantities, locations, indoor/outdoor, mounting, sync method, failure indication, environmental ratings.
10. **Transmission/frequency boundary** — define handover between time-of-day distribution and transport frequency/phase synchronisation (Rule 2).
11. **Hazardous-area and environmental provisions** — classified-area antenna and equipment siting (O&G), outdoor antenna environment (rail and O&G), certification applicability.
12. **Antenna, lightning and cable provisions** — mast/roof provisions, surge protection, cable type and maximum run, delay compensation.
13. **Monitoring and NMS scope** — offset monitoring at consumers, GNSS-quality alarms, integration to the control room.
14. **Power and environment** — UPS/DC supply, autonomy, cooling and space per site type.
15. **Cybersecurity and vendor compliance** — NTP authentication, PTP rogue-master protection, GNSS jamming/spoofing detection, segmentation, banned-vendor-list check (Rule 8).
16. **Safety boundary** — confirm which consumers, if any, are safety-related and specify the interface (Rule 7).
17. **Interfaces** — grouped by family: **transport** (frequency/phase), **control** (SCADA/DCS/ESD, signalling), **security/video** (CCTV), **voice and alarm** (PAGA, PABX), **radio** (GSM-R, TETRA NMS), **passenger information and ticketing**, **enterprise IT**.
18. **Compliance matrix** — map each requirement to IEEE, IETF, ITU-T, IEC and IRIG references (`standards.md`).
19. **Tender-grade BOQ and acceptance criteria** — BOQ basis; acceptance tests (offset vs reference, holdover, failover, GNSS-loss and recovery, display-clock agreement).
20. **Verification and commissioning strategy** — test sequence, reference instrument and its traceability, who witnesses.

*(Harish: correct the order, flag anything missing or misplaced — same ask as the other subsystems. Items 1 and 10 (accuracy budget and the time/frequency boundary) are the ones I'd most like a practising time-sync engineer to check.)*

- **Inputs:** Stage 1 outputs; PMC's oversight/format requirements; hazardous-area data (O&G); any banned-vendor or constellation restriction; client IT/OT network standards.
- **Decisions:** the 20-point sequence above; accuracy budgets refined from parametric to specification-grade.
- **Deliverables:** technical specification, consumer accuracy matrix, time policy, compliance matrix, tender BOQ, acceptance criteria, ICD requirement list.
- **Roles:** Consultant authors; PMC reviews; Client approves; Vendor/OEM supplies indicative data under the OEM-sourcing rule.
