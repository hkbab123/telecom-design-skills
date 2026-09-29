# Stage 3 — Engineering (post-award, detailed design)

The contract has been awarded. The Stage 2 technical specification is now the **binding contract requirement**. The Contractor/System Integrator is the primary producer at this stage; the Consultant/PMC shift into a review/compliance-checking role; the OEM/Vendor supplies vendor-specific technical documents the detailed design is built around.

## Detailed engineering sequence

1. **Contract/spec kick-off and compliance baseline** — review the awarded technical specification and Stage 2 compliance matrix line by line; raise any RFI or deviation/technical-query log before design starts; confirm the SIS-boundary/fire-life-safety scope and hazardous-area zoning from Stage 2 as fixed inputs, not open items.
2. **Vendor/OEM confirmation and vendor document intake** — final equipment vendor confirmed (from the Approved Vendor List or per contract award); obtain the vendor's standard technical documentation package (datasheets, ATEX/IECEx certificates, protocol conformance statements). **Apply the OEM-sourcing rule from here on**: every OEM-specific parameter must trace to one of these documents, never invented.
3. **Detailed site survey** — walkover/detailed survey per site: field-device locations, cabinet/panel positions, cable-routing conditions, power availability. For O&G, this survey must be coordinated with the site's permit-to-work system and conducted by personnel qualified to enter the relevant hazardous-area zones; confirm the hazardous-area classification drawing against actual site conditions before finalising equipment siting.
4. **Detailed I/O list and signal database finalisation** — actual point-by-point I/O list per RTU/PLC, tag database, and engineering units, taken off the confirmed field-device list.
5. **Control logic design (normal mode)** — detailed control narrative and logic diagrams for normal-mode operation (rail: airflow/CO-driven fan control; O&G: process-control loops), including setpoints and interlocks that are SCADA/DCS-level (not SIS-level) by definition.
6. **Control logic design (emergency/fire mode or degraded mode)** — detailed control narrative and logic diagrams for the fire/emergency-mode sequence (rail tunnel ventilation, per the governing fire/life-safety code) or degraded-mode operation (O&G), reviewed and, where required, independently verified as a distinct deliverable from normal-mode logic (Subsystem-specific rule 4).
7. **SIS/ESD interface detailed design (O&G, where applicable)** — the specific signals, protocol, and independence measures at the SIS-to-SCADA boundary defined in Stage 2 item 2, engineered in detail; confirm the interface remains one-way status/alarm unless a specific, independently justified exception exists.
8. **Network architecture and IT/OT segmentation detailed design** — actual zone/conduit implementation (firewall rules, DMZ server placement, remote-access mechanism) per the Stage 2 IEC 62443 model; network diagrams showing every OT-to-IT crossing point.
9. **Redundancy implementation** — actual SCADA server hot-standby configuration, RTU/PLC redundancy (where specified), network redundancy (ring/dual-homed) implemented against real site topology.
10. **Communication protocol detailed configuration** — actual protocol parameters (polling intervals, timeout/retry settings, IEC 60870-5-104 station addresses or equivalent) configured per the Stage 2 protocol selection.
11. **Equipment dimensioning and selection (final)** — actual OEM part numbers/models for SCADA servers, engineering workstations, RTU/PLC panels (confirming ATEX/IECEx certificate applicability per unit and per zone), historian server, network switches/routers, HMI consoles — every figure sourced to a vendor datasheet/certificate or marked "confirm with OEM."
12. **Power system design per site** — UPS/battery autonomy calculation for the control room and each RTU/PLC cabinet, sized against the actual equipment load from step 11.
13. **HMI graphics and historian configuration design** — actual screen hierarchy build-out per the Stage 2 philosophy, alarm configuration against the Stage 2 EEMUA 191-based rationalisation, historian tag list and retention configuration.
14. **Interface Control Documents (ICDs)** — one per interface family from the Stage 2 interfaces checklist (SIS/fire-alarm boundary, telecom systems, enterprise systems, other building/plant systems) — each ICD defines the actual protocol, data format, and physical/logical connection point with the other system's owner.
15. **Reliability/safety-case evidence (detailed)** — evidence against the numeric KPIs fixed at Stage 2 (availability, MTBF/MTTR, alarm response time); for the fire/life-safety or SIS-adjacent function, the detailed evidence against the framework referenced in Stage 2 item 15.
16. **Hazardous-area installation design (O&G)** — cable entry/gland certification, junction box and enclosure Ex-rating verification, equipotential bonding and earthing design per the applicable hazardous-area installation standard, independent of the equipment certification already confirmed in step 11.
17. **System block diagrams and drawings package** — architecture/block diagram, network diagram (with IT/OT boundary marked), panel layout drawings, cable/routing schedules, and (for O&G) hazardous-area zoning drawings overlaid with equipment siting.
18. **Technical specification (as-designed) and datasheet/certificate compilation** — Contractor's own technical specification restating the awarded requirement against the actual design, plus compiled equipment datasheets and ATEX/IECEx certificates (referenced, not re-typed).
19. **Bill of Quantities (final)** — quantities taken off the finalised design, priced against the contract.
20. **Test and commissioning plan (FAT/SAT)** — factory and site acceptance test procedures, tracing back to the tender-grade acceptance criteria fixed at Stage 2, with a dedicated loop-test methodology for every I/O point, a dedicated emergency-mode/fire-mode functional test (rail) or SIS-interface verification test (O&G), and cybersecurity configuration verification against the IEC 62443 model.
21. **As-built documentation and O&M handover** (post-installation, closing sub-phase) — as-built drawings, O&M manuals, training records, spares provisioning list, and a compiled hazardous-area equipment certificate register for O&G sites.

## Document gating (starting points — verify against your project's actual gate structure)

- The SIS-boundary/fire-life-safety scope definition (step 1) gates control-logic design (steps 5–7) — don't proceed with emergency-mode logic ahead of it.
- Hazardous-area zoning confirmation (step 3) gates equipment dimensioning (step 11) and installation design (step 16) for O&G sites.
- Vendor documents (step 2) gate every OEM-sourced figure in steps 9–19.
- IT/OT network architecture (step 8) typically needs Client/PMC IT-security sign-off before commissioning (step 20) proceeds.
- ICDs (step 14) typically need the other system's owner to countersign before drawings (step 17) proceed.
- Emergency-mode/fire-mode functional testing (step 20) is independent of, and in addition to, normal-mode loop testing — both must pass, neither substitutes for the other.

## Inputs

Awarded technical specification, Stage 2 compliance matrix, confirmed OEM/vendor documents, detailed survey data, hazardous-area classification drawing (O&G), governing fire/life-safety code (rail tunnel ventilation).

## Deliverables (multi-document)

- Technical specification (as-designed)
- Datasheets and ATEX/IECEx certificates
- Bill of Quantities
- System block diagram / drawings package, including network (IT/OT) and hazardous-area zoning overlays
- Control narratives and logic diagrams (normal mode and emergency/degraded mode, separately)
- Detailed survey report
- Interface Control Documents
- Reliability/safety-case evidence
- Test and commissioning (FAT/SAT) plan, including emergency-mode/SIS-interface verification
- As-built documentation, O&M manuals, and hazardous-area certificate register

## Roles

- **Contractor/System Integrator** — primary producer of the full engineering package
- **PMC/Consultant** — review submittals for compliance against the Stage 2 spec
- **Client** — reviews/approves at contract-defined gates
- **Vendor/OEM** — supplies the technical documents and certificates the detailed design is built on
