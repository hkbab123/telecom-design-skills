# Stage 3 — Engineering (post-award, detailed design)

Contract awarded to the Contractor/System Integrator; the Stage 2 spec becomes the binding contract requirement; Consultant/PMC shift to a review/compliance role; OEM/Vendor supplies vendor-specific technical documents.

## Draft ordered sequence

1. **Contract/spec kick-off and compliance baseline** — review the awarded spec and Stage 2 compliance matrix line by line; raise an RFI/deviation log before design starts; confirm hazardous-area zoning data, the PA/GA zone split, and the SIL determination (if any) from Stage 2 as fixed inputs, not open items.
2. **Vendor/OEM confirmation and vendor document intake** — final vendor confirmed (AVL or per award); obtain the vendor's technical documentation package (amplifier/loudspeaker datasheets, ATEX/IECEx certificates, fire-survival cable certification, interface specs). **OEM-sourcing rule applies from here**: every OEM-specific parameter must trace to a vendor document, never invented.
3. **Detailed site survey** — walkover/detailed survey per building/zone: exact loudspeaker mounting locations, cable routing, power availability, existing infrastructure conflicts, and an **ambient noise measurement survey per zone** (the actual input the acoustic model in step 5 needs, replacing the Stage 2 estimate). For O&G, coordinate with the site's permit-to-work system and confirm the classification drawing against actual site conditions before finalising equipment siting.
4. **Detailed zone plan finalisation** — actual PA and GA zone boundaries confirmed against the surveyed building/plant layout, reconciling Stage 2's zone philosophy with real architectural/structural constraints.
5. **Detailed acoustic modelling** — SPL and STI/CIS calculation per zone using actual room/area acoustic data (reverberation, structural clutter/absorption for dense plant areas vs open outdoor areas) and the surveyed ambient noise level from step 3, refining Stage 2's target into a verified loudspeaker layout and count per zone.
6. **Detailed system architecture and rack/amplifier siting** — actual equipment rack and amplifier siting per Stage 2's architecture choice, with redundancy (item 5 of Stage 2) implemented against real equipment room locations.
7. **Loudspeaker circuit and cable-loading finalisation** — final constant-voltage line design, tap loading per amplifier circuit, and voltage-drop calculation per actual cable run length using vendor cable/amplifier specs from step 2.
8. **Equipment dimensioning and selection (final)** — actual OEM part numbers for amplifiers, loudspeakers/horns (confirming ATEX/IECEx certificate applicability per unit/zone), control panels/call stations, and power supplies — every figure sourced or marked "confirm with OEM."
9. **Power system design** — UPS/battery autonomy calculation against the actual connected load and the fire-code-driven autonomy target from Stage 2 item 10; generator sizing where required (e.g. remote O&G field sites without grid connection).
10. **Cabling detailed design** — fire-survival cable routing and segregation per the applicable fire code, line/loop supervision circuit design (Stage 2 item 9) implemented against the actual cable topology, cable schedules.
11. **Functional safety detailed design and verification (where SIL-rated)** — if Stage 2 item 6 determined a SIL rating applies, produce the detailed functional-safety design and verification evidence per IEC 61508/61511 — proof-test intervals, diagnostic coverage, independent supervision — as a distinct deliverable from the general reliability case (item 13).
12. **Interface Control Documents (ICDs)** — one per interface family from the Stage 2 checklist (Fire Alarm Control Panel, Fire & Gas/ESD, PABX, SCADA/NMS, CCTV, passenger information system) — protocol, data format, physical/logical connection point, and — critically for the F&G/ESD interface — the exact trigger logic and timing for automatic GA activation on a confirmed event, countersigned by that system's owner.
13. **Reliability/safety case (detailed)** — evidence against the numeric KPIs from Stage 2 item 15; where GA is SIL-rated, this sits alongside (not instead of) the dedicated functional-safety verification package from step 11.
14. **Hazardous-area installation design (O&G)** — cable entry/gland certification, junction box/enclosure Ex-rating verification, equipotential bonding/earthing per the applicable hazardous-area installation standard (e.g. IEC 60079-14) — independent of equipment certification (step 8); installation practice inside a classified zone has its own compliance requirements beyond "the equipment itself is certified."
15. **System block diagrams and drawings package** — architecture/block diagram, zone layout drawings with loudspeaker/horn positions, rack/cabinet layout, cable/routing schedules, and (O&G) hazardous-area zoning drawings overlaid with equipment siting.
16. **Technical specification (as-designed) and datasheet/certificate compilation** — Contractor's own spec restating the awarded requirement against the actual design, plus compiled datasheets, ATEX/IECEx certificates, and fire-survival cable certification.
17. **Bill of Quantities (final)** — quantities off the finalised design, priced against the contract.
18. **Test and commissioning plan (FAT/SAT)** — FAT/SAT procedures tracing to the tender-stage acceptance criteria: SPL/STI verification per zone against the acoustic model (step 5), loop-supervision fault-injection test, F&G/ESD-triggered automatic activation test, battery-autonomy discharge test, and — where SIL-rated — the functional-safety proof-test procedure from step 11.
19. **As-built documentation and O&M handover** *(post-installation closing sub-phase)* — as-built drawings, O&M manuals, training records, spares list, and a compiled hazardous-area equipment certificate register for O&G sites.

## Document gating (starting points)

- Hazardous-area zoning confirmation (step 3) gates every subsequent equipment and installation decision for O&G sites.
- Vendor documents (step 2) gate every OEM-sourced figure in steps 5–17.
- The ambient noise survey (step 3) gates the acoustic model (step 5), which in turn gates final loudspeaker selection (step 8) and BOQ (step 17).
- F&G/ESD ICD (step 12) needs that system's owner to countersign before the automatic-activation test (step 18) can be designed and executed.
- Functional-safety verification (step 11) and hazardous-area installation design (step 14) are both independent inputs Test & Commissioning (step 18) must verify jointly.

## Inputs

Awarded spec, Stage 2 compliance matrix, confirmed OEM/vendor documents, detailed survey data (incl. ambient noise), hazardous-area classification drawing (O&G).

## Deliverables

Technical spec (as-designed), datasheets/certificates, BOQ, block diagram/drawings incl. hazardous-area overlay, acoustic model/coverage study, survey report (incl. ambient noise), ICDs, reliability/safety case, functional-safety verification package (where SIL-rated), FAT/SAT plan, as-built docs + certificate register.

## Roles

- **Contractor/SI** produces the full package
- **PMC/Consultant** review for compliance
- **Client** approves at gates
- **Vendor/OEM** supplies documents/certificates
