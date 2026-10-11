# Engineering Stage — Master Clock / Time Synchronisation

Contractor/SI-led detailed post-award design. Consultant/PMC review for compliance; OEM/Vendor supplies vendor-specific data.

**Draft ordered sequence (first-pass domain reconstruction, no project reference behind it yet):**

1. **Contract/spec kick-off** — confirm the awarded spec and Stage 2 compliance matrix; confirm the time policy, consumer accuracy matrix, hazardous-area zoning and any vendor or constellation restriction as fixed inputs.
2. **Vendor/OEM document intake** — datasheets for master clocks, GNSS receivers, oscillator holdover specifications, display clocks, ATEX/IECEx certificates where applicable. **OEM-sourcing rule applies here.**
3. **Consumer survey and confirmation** — confirm each consumer's actual time interface (NTP, PTP profile, IRIG-B, serial, impulse) and its real timestamp resolution with the consumer's owner; update the accuracy matrix.
4. **Site and antenna survey** — sky view, multipath, mounting structure, cable route, lightning exposure, zoning; for O&G, coordinate permit-to-work and confirm zoning against actual site conditions.
5. **Reference and hierarchy design** — master/sub-master locations, source-priority order, holdover plan, second-reference design where in scope.
6. **Accuracy budget sheets** — per consumer: reference error, antenna cable delay, distribution error (NTP root distance or PTP path asymmetry and on-path error), consumer resolution; compare to requirement (`fundamentals/09-accuracy-requirements-by-consumer.md`).
7. **Network design for time** — VLAN/QoS plan, PTP profile and clock-class settings, boundary/transparent clock placement, NTP server list per consumer, asymmetry controls.
8. **Display clock design** — quantities, positions, mounting, sync method, failure indication, daylight-saving behaviour.
9. **Legacy distribution design** — IRIG-B/1PPS/serial/impulse runs, signal levels, distribution amplifiers, cable lengths and delay compensation.
10. **Redundancy and failover configuration** — hot-standby pairing, priority settings, maximum step on switchover, split-brain resolution rule.
11. **Monitoring design** — offset monitors, GNSS-quality alarms, alarm mapping to the control room, trending (`fundamentals/12-monitoring-nms-fault-handling.md`).
12. **Cybersecurity detailed configuration** — NTP authentication keys or NTS, PTP port roles and rogue-master protection, disabled services, ACLs, segmentation, firmware baseline, banned-vendor compliance on the actual selected equipment.
13. **Power, antenna and environment design** — UPS/DC load per site, antenna lightning protection and grounding, cable and amplifier selection, rack space and cooling.
14. **Interface control documents (ICDs)** — one per interfacing subsystem (`fundamentals/16-interfacing-other-subsystems.md`), signed by the counterpart subsystem owner.
15. **Equipment dimensioning and final selection** — actual OEM part numbers, with certification applicability per unit/zone where relevant.
16. **Design documents and drawings** — architecture block diagram, time-distribution topology, antenna and cable schedules, display-clock location drawings, rack and panel layouts.
17. **FAT plan** — offset against a traceable reference, holdover behaviour, failover step size, GNSS-loss and recovery, protocol conformance on factory equipment.
18. **Installation and cable-delay verification** — antenna installation records, measured cable delay entered into receiver configuration, per-run IRIG/serial checks.
19. **SAT/commissioning plan** — end-to-end offset at every consumer class, holdover and failover on site, GNSS-loss simulation, daylight-saving and leap-second behaviour test, display-clock agreement walk-through, monitoring integration.
20. **Handover and as-built** *(post-installation sub-phase)* — as-built antenna and cable records, final configuration backups, test records, spares and maintenance manual.

*(Harish: first-pass reconstruction — please correct the order, flag gating dependencies, and sanity-check especially step 3 (consumer confirmation) and step 6 (accuracy budget) once you're ready to share any project reference material.)*

**Document gating (starting points):**
- Consumer survey (step 3) gates the accuracy budget (step 6) and the network design (step 7).
- Site and antenna survey (step 4) gates the reference design (step 5) and power/antenna design (step 13).
- Vendor documents (step 2) gate OEM-sourced figures in steps 5–15.
- ICDs (step 14) typically need the counterpart owner's countersignature before drawings (step 16) proceed.
- Cable-delay verification (step 18) gates SAT offset measurements (step 19).

- **Inputs:** awarded spec, Stage 2 compliance matrix, confirmed OEM/vendor documents, survey data, hazardous-area classification drawing (O&G).
- **Deliverables:** technical spec (as-designed), datasheets/certificates, BOQ, architecture and distribution drawings, antenna and cable schedules, accuracy budget sheets, network and security configuration, monitoring design, ICDs, FAT/SAT plan, as-built documents.
- **Roles:** Contractor/SI produces the full package; PMC/Consultant review compliance; Client approves gates; Vendor/OEM supplies documents and certificates.
