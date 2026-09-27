# Stage 3 — Engineering (post-award, detailed design)

The contract has been awarded. The Stage 2 technical specification is now the **binding contract requirement**. The Contractor/System Integrator is the primary producer at this stage; the Consultant/PMC shift into a review/compliance-checking role; the OEM/Vendor supplies vendor-specific technical documents the detailed design is built around.

## Detailed engineering sequence

1. **Contract/spec kick-off and compliance baseline** — review the awarded technical specification and Stage 2 compliance matrix line by line; raise any RFI or deviation/technical-query log before design starts; confirm the hazardous-area zoning data and DMO/encryption decisions from Stage 2 as fixed inputs, not open items.
2. **Vendor/OEM confirmation and vendor document intake** — final equipment vendor confirmed (from the Approved Vendor List or per contract award); obtain the vendor's standard technical documentation package (datasheets, ATEX/IECEx certificates, interface specs). **Apply the OEM-sourcing rule from here on**: every OEM-specific parameter must trace to one of these documents, never invented.
3. **Detailed site survey** — walkover/detailed survey per site: exact site coordinates, mast/tower or building-mount conditions, power availability, existing infrastructure conflicts. For O&G, this survey must be coordinated with the site's permit-to-work system and conducted by personnel qualified to enter the relevant hazardous-area zones; confirm the hazardous-area classification drawing against actual site conditions (zoning can change as plant configuration changes) before finalising equipment siting.
4. **Detailed frequency plan and spectrum licence finalisation** — actual frequency/channel assignment obtained from the regulator for the confirmed site list.
5. **Detailed SwMI architecture and site list finalisation** — actual exchange/switch siting, base station site list, and redundancy implementation finalised against real sites.
6. **Detailed coverage prediction (the Coverage Study)** — RF planning tool output using actual site coordinates, terrain/clutter data (or, for O&G plant, actual structural/plant layout data — process plant propagation modelling is materially different from open terrain and should use a model suited to dense industrial clutter, not a generic outdoor model); refines Stage 2's coverage philosophy into predicted coverage maps per site and per special area, including in-building/in-plant predictions.
7. **Detailed link budget** — path loss, fade margin, cable/combiner losses recalculated per actual site using vendor equipment specs from step 2.
8. **Capacity/traffic dimensioning finalisation** — Erlang modelling refined with actual expected call-attempt data per talkgroup, confirming traffic channel count per site.
9. **Equipment dimensioning and selection (final)** — actual OEM part numbers/models for base stations, SwMI exchange, dispatcher consoles, handheld/mobile radios (confirming ATEX/IECEx certificate applicability per unit and per zone), DMO gateways/repeaters, site cabinets and power systems — every figure sourced to a vendor datasheet/certificate or marked "confirm with OEM."
10. **Power system design per site** — UPS/battery autonomy calculation, generator sizing where required (particularly for remote O&G field sites without grid connection), sized against the actual site list and equipment load from step 9.
11. **Transmission/backhaul detailed design** — actual link design (fibre, microwave, or leased circuit) between confirmed sites and the SwMI core, bandwidth allocation against the dimensioned traffic.
12. **Interface Control Documents (ICDs)** — one per interface family from the Stage 2 interfaces checklist (telephony/PABX gateway, SCADA/alarm, maintenance-management, dispatcher/control-room, any adjacent radio network) — each ICD defines the actual protocol, data format, and physical/logical connection point with the other system's owner.
13. **Reliability/safety case (detailed)** — evidence against the numeric KPIs fixed at Stage 2 (availability, MTBF/MTTR, coverage %, call setup time); for O&G, the detailed functional-safety evidence against the framework referenced in Stage 2 item 15, if TETRA carries emergency-response or process-safety-linked traffic.
14. **Hazardous-area installation design (O&G)** — cable entry/gland certification, junction box and enclosure Ex-rating verification, equipotential bonding and earthing design per the applicable hazardous-area installation standard (e.g. IEC 60079-14), independent of the equipment certification already confirmed in step 9 — installation practice inside a classified zone has its own compliance requirements beyond "the equipment itself is certified."
15. **System block diagrams and drawings package** — architecture/block diagram, site layout drawings, rack/cabinet layout, cable/routing schedules, and (for O&G) hazardous-area zoning drawings overlaid with equipment siting.
16. **Technical specification (as-designed) and datasheet/certificate compilation** — Contractor's own technical specification restating the awarded requirement against the actual design, plus compiled equipment datasheets and ATEX/IECEx certificates (referenced, not re-typed).
17. **Bill of Quantities (final)** — quantities taken off the finalised design, priced against the contract.
18. **Test and commissioning plan (FAT/SAT)** — factory and site acceptance test procedures, tracing back to the tender-grade acceptance criteria fixed at Stage 2, including verification that installed hazardous-area equipment matches its certified configuration (a common non-compliance point: correctly certified equipment installed or modified in a way that invalidates the certificate).
19. **As-built documentation and O&M handover** (post-installation, closing sub-phase) — as-built drawings, O&M manuals, training records, spares provisioning list, and a compiled hazardous-area equipment certificate register for O&G sites.

## Document gating (starting points — verify against your project's actual gate structure)

- Hazardous-area zoning confirmation (step 3) gates every subsequent equipment and installation decision for O&G sites — don't proceed to equipment dimensioning (step 9) or installation design (step 14) ahead of it.
- Vendor documents (step 2) gate every OEM-sourced figure in steps 6–17.
- The Coverage Study (step 6) typically needs Client/PMC sign-off before Equipment Dimensioning (step 9) and BOQ (step 17) are finalised.
- ICDs (step 12) typically need the other system's owner to countersign before drawings (step 15) proceed.
- Hazardous-area installation design (step 14) and equipment certification (step 9) are both independent inputs Test & Commissioning (step 18) must verify jointly — a certified device installed non-compliantly is still a non-compliance.

## Inputs

Awarded technical specification, Stage 2 compliance matrix, confirmed OEM/vendor documents, detailed survey data, hazardous-area classification drawing (O&G).

## Deliverables (multi-document)

- Technical specification (as-designed)
- Datasheets and ATEX/IECEx certificates
- Bill of Quantities
- System block diagram / drawings package, including hazardous-area zoning overlay
- Coverage study
- Detailed survey report
- Interface Control Documents
- Reliability/safety case
- Test and commissioning (FAT/SAT) plan
- As-built documentation, O&M manuals, and hazardous-area certificate register

## Roles

- **Contractor/System Integrator** — primary producer of the full engineering package
- **PMC/Consultant** — review submittals for compliance against the Stage 2 spec
- **Client** — reviews/approves at contract-defined gates
- **Vendor/OEM** — supplies the technical documents and certificates the detailed design is built on
