# Stage 2 — Tender (client requirement development)

This is where this skill's core value sits: helping the engineer build the SCADA technical requirement specification by combining the applicable standards/inputs carried over from Concept with SCADA/control-systems know-how.

## Actors and sequence

1. PMC + specialized SCADA/control-systems Consultant engaged by client.
2. Consultant takes **Stage 1 outputs as input**: applicable standards, stakeholder requirements, high-level proposal/architecture direction, SIS-boundary or fire/life-safety-scope findings.
3. Consultant **builds the SCADA technical specification**, working through the decision sequence below.
4. Completed specification becomes part of the **tender package** contractors/system integrators bid against.
5. In parallel, the Consultant goes back to the market for **more accurate pricing**.
6. This results in an **Approved Vendor List (AVL)** and typically OEM/integrator shortlisting.

## Technical specification decision sequence

Work through these in order.

1. **Scope and functional boundary** — list every system SCADA will supervise/control: for rail, tunnel-ventilation fans/dampers/sensors, station pumps, escalator/lift status monitoring, HVAC; for O&G, process areas, wellsites, pipeline stations. Explicitly state what is **out of scope** — most importantly, the boundary with any SIS/ESD system (O&G) or fire alarm/life-safety system (rail) — SCADA may monitor/receive status from these, but must not implement their safety logic.
2. **SIS/ESD or fire/life-safety interface (do this early, not late)** — if Subsystem-specific rule 1/4 applies, define the interface point precisely: what data crosses from the SIS/fire system to SCADA (status/alarm only, one-way) versus any control signal that might cross the other way (should be minimal to none, and independently reviewed). This constrains the architecture for the rest of the sequence.
3. **Hazardous-area zoning and equipment certification (O&G)** — obtain or commission the site's hazardous-area classification drawing; every field instrument, RTU, junction box, and cabling item sited in a classified zone must carry the matching ATEX/IECEx certification. Flag this as a hard gate on item 10 (equipment dimensioning).
4. **System architecture** — centralised SCADA (single control room, RTUs/PLCs reporting up) vs distributed/hierarchical architecture (local control rooms per station/plant area with a central supervisory layer); number and siting of SCADA servers, engineering workstations, and RTU/PLC panels; historian and reporting server placement.
5. **Control philosophy — normal vs emergency/degraded modes** — for rail tunnel ventilation, explicitly define the normal-mode control sequence (air-quality/CO-driven fan control) separately from the fire/emergency-mode sequence (jet-fan reversal/smoke-extraction logic per the governing fire/life-safety code); for O&G, define normal process-control sequences separately from any degraded/emergency operating modes SCADA must support (recognising these are distinct from SIS trip logic).
6. **IT/OT network segmentation and cybersecurity architecture** — define the IEC 62443 zone and conduit model for this deployment: OT network(s), DMZ, and IT network, with the conduits (firewalls, data diodes where appropriate) between them; remote-access policy; patch-management and antivirus strategy appropriate to an OT environment (not a blind copy of the corporate IT policy).
7. **Redundancy and availability targets** — network-level availability target (state explicitly per use case — rail tunnel-ventilation emergency-mode reliability is not the same target as a station pump-monitoring convenience function); SCADA server redundancy (hot-standby pair); RTU/PLC redundancy where justified; network redundancy (ring, dual-homed).
8. **Communication protocols** — select the protocol(s) for field-to-RTU/PLC (Modbus, hardwired I/O) and RTU/PLC-to-SCADA (IEC 60870-5-101/104 — common in rail/utility telecontrol, DNP3, OPC-UA, Modbus TCP); state why, based on the field device population and any legacy protocol already in use (brownfield).
9. **I/O count and signal list basis** — approximate digital/analogue I/O point count per site/RTU, derived from the field device list in item 1; signal list format and tag-naming convention.
10. **Equipment dimensioning and selection basis** — SCADA server sizing, engineering workstation count, RTU/PLC panel count and I/O capacity per site (including which units must be ATEX/IECEx-certified per item 3), historian server sizing, network switch/router count, HMI/operator-console count for the control room.
11. **Alarm management philosophy** — reference EEMUA 191 alarm-rationalisation principles at the specification stage: alarm priority classes, target alarm rate per operator per hour, avoidance of nuisance/flood alarms — don't leave alarm design as an afterthought bidders fill in however they like.
12. **HMI and historian requirements** — operator screen hierarchy (overview/area/detail), trending and reporting requirements, data retention period for the historian, and any regulatory/audit data-retention requirement.
13. **Interfaces** — list explicitly, by family: **safety systems** (the SIS/ESD or fire-alarm boundary from item 2); **telecom systems** (SCADA ↔ TETRA/GSM-R for alarm/status relay, SCADA ↔ PAGA for automated announcement triggering); **enterprise systems** (SCADA ↔ maintenance-management/CMMS, SCADA ↔ MES/ERP if in scope per ISA-95); **other building/plant systems** (BMS, fire alarm, access control) — for each, state direction of data flow and protocol.
14. **Regulatory approvals** — any regulatory sign-off required for the fire/life-safety emergency-mode function (rail) or process-safety interface (O&G); data-retention/audit requirements from the relevant authority.
15. **Availability/reliability KPIs and safety-case basis** — numeric targets bidders must commit to (system availability %, MTBF/MTTR, alarm response time, historian data-capture reliability). Where a fire/life-safety or SIS-adjacent function is in scope, reference the client's applicable functional-safety framework (IEC 61508/61511-derived, or the governing fire/life-safety code) rather than assuming a generic SCADA reliability target covers it.
16. **Compliance matrix** — map every requirement above to the relevant standard clauses (IEC 62443, IEC 61508/61511, IEC 60870-5, the applicable fire/life-safety code) and the client's own requirement register.
17. **Tender-grade BOQ and testing/acceptance criteria** — high-level bill of quantities basis; FAT/SAT acceptance criteria bidders must commit to, including a specific emergency-mode/fire-mode functional test requirement for rail tunnel ventilation, or a SIS-interface verification test for O&G.
18. **Verification & commissioning strategy** — pre-commissioning test approach, including loop testing methodology and how emergency-mode/SIS-boundary testing will be independently witnessed.

## Inputs

Stage 1 outputs; PMC's oversight requirements/format standards; hazardous-area classification data (O&G); fire/life-safety code applicable to the project's jurisdiction (rail tunnel ventilation).

## Deliverables

SCADA technical specification (for tender), refined/accurate pricing data, Approved Vendor List, OEM/platform selection outcome, compliance matrix against standards.

## Roles

- **Consultant** — builds the technical specification, runs the refined market pricing exercise
- **PMC** — oversees the Consultant's deliverables on the client's behalf
- **Client** — engages PMC + Consultant, ultimately owns the resulting tender
- **Contractor** — bids against the tender package
- **Vendor/OEM/SI** — provides accurate pricing, ends up on the Approved Vendor List

All figures in this file (I/O counts, alarm rates, reliability targets) are illustrative and project/jurisdiction-dependent — confirm the actual applicable figure or standard clause against the governing spec, national regulator, and (for rail tunnel ventilation) the applicable fire/life-safety code for each project.
