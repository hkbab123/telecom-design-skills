# Stage 3 — Engineering (post-award, detailed design)

The contract has been awarded to the **EPC Contractor**. The Stage 2 technical specification is now the **binding contract requirement** — it stops being negotiable and becomes the thing everything downstream must be shown to comply with. The Contractor is the primary producer at this stage; the Consultant/PMC shift into a review/compliance-checking role; the OEM/Vendor (now selected off the Approved Vendor List, or per contract) supplies vendor-specific technical documents the Contractor's detailed design is built around.

## The 20-step detailed engineering sequence

1. **Contract/spec kick-off and compliance baseline** — review the awarded technical specification and Stage 2 compliance matrix line by line; raise any request-for-clarification (RFI to Client/PMC) or deviation/technical-query log before design starts; confirm the cross-border core-placement decision (if applicable) and any other Stage 2 architecture decisions as fixed inputs, not open items.
2. **Vendor/OEM confirmation and vendor document intake** — final equipment vendor confirmed (from the Approved Vendor List or per contract award); obtain the vendor's standard technical documentation package (datasheets, interface specs, standard drawings) as the factual basis for detailed design. **Apply the OEM-sourcing rule from here on**: every OEM-specific parameter used must trace to one of these vendor documents, never invented.
3. **Detailed site survey** — walkover/detailed survey per site (not the order-of-magnitude Stage 1 survey): exact site coordinates, mast/tower foundation and access conditions, power availability, existing infrastructure/utility conflicts, tunnel/station-specific constraints, land/way-leave status.
4. **Detailed frequency plan and spectrum licence application** — actual frequency assignment requested/obtained from the regulator(s) for the confirmed site list; cross-border frequency coordination finalised with the neighbouring administration if applicable.
5. **Detailed network architecture and site list finalisation** — actual BSC/MSC/core siting, IP addressing/numbering plan finalised against real sites; cross-border core-placement decision implemented into an actual node/site list, not re-decided here.
6. **Detailed cell planning and coverage prediction (the Coverage Study)** — RF planning tool output using actual site coordinates, terrain/clutter data, antenna heights/orientation; refines Stage 2's coverage philosophy into predicted field-strength/handover maps per site and per special area.
7. **Detailed link budget** — path loss, fade margin, RF aging margin, cable/combiner losses recalculated per actual site (tunnel leaky-feeder runs, discrete antenna sites) using vendor equipment specs from step 2.
8. **Capacity/traffic dimensioning finalisation** — Erlang modelling refined with actual train-service timetable/frequency data, confirming TRX count and, if in scope, packet-core (SGSN/GGSN/PCU) sizing per site.
9. **Equipment dimensioning and selection (final)** — actual OEM part numbers/models for BTS/BSC/MSC/gateway, dispatcher workstations, cab radios/SIMs (against confirmed rolling-stock fleet size), trackside cabinets and power systems — every figure sourced to a vendor datasheet or marked "confirm with OEM."
10. **Power system design per site** — UPS/battery autonomy calculation, generator sizing where required, sized against the actual site list and equipment load from step 9.
11. **Transmission/backhaul detailed design** — actual fibre route/ring design or microwave link design between confirmed sites, bandwidth allocation against the dimensioned traffic.
12. **Interface Control Documents (ICDs)** — one per interface family from the Stage 2 interfaces checklist (signalling/RBC, transmission backbone, O&M/asset systems, legacy telecom, public network, power, cross-border, rolling stock) — each defines the actual protocol, data format, and physical/logical connection point with the other system's owner.
13. **RAMS / safety case (detailed)** — hazard log, safety integrity level substantiation, and evidence against the numeric RAMS KPIs fixed at Stage 2; Independent Safety Assessor engagement where the contract requires one.
14. **Cybersecurity detailed design** — actual network segmentation, encryption/key-management implementation, and firewall/access-control design against the cybersecurity standard fixed at Stage 2.
15. **System block diagrams and drawings package** — architecture/block diagram, single-line diagrams, site layout drawings, rack/cabinet layout, cable/routing schedules — the visual expression of steps 5–12.
16. **Technical specification (as-designed) and datasheet compilation** — Contractor's own technical specification restating the awarded requirement against the actual design, plus the compiled set of equipment datasheets (vendor documents from step 2, referenced not re-typed).
17. **Bill of Quantities (final)** — quantities taken off the finalised design (steps 5–15), priced against the contract.
18. **Tools list / test-equipment requirements** — tools and test equipment the installation/commissioning team needs, driven by the equipment list from step 9 and the test plan in step 19.
19. **Test and commissioning plan (FAT/SAT)** — factory acceptance and site acceptance test procedures and criteria, tracing back to the tender-grade acceptance criteria fixed at Stage 2 and the RAMS/QoS verification strategy.
20. **As-built documentation and O&M handover** (post-installation — a distinct closing sub-phase, not part of the design-production sequence above) — as-built drawings, O&M manuals, training records, spares provisioning list.

## Document gating (starting points — verify against your project's actual gate structure)

- Vendor documents (step 2) gate every OEM-sourced figure in steps 6–17 — don't finalise link budget, capacity, equipment dimensioning, or BOQ ahead of vendor confirmation.
- The Coverage Study (step 6) and detailed link budget (step 7) typically need Client/PMC sign-off before Equipment Dimensioning (step 9) and BOQ (step 17) are finalised, since they drive equipment counts.
- ICDs (step 12) typically need the other system's owner (signalling authority, SCADA owner, etc.) to countersign before drawings (step 15) proceed, since drawings depend on confirmed interface points.
- RAMS/safety case (step 13) and cybersecurity design (step 14) are usually independent, parallel workstreams to steps 6–12 rather than sequential blockers — but both must close out before Test & Commissioning (step 19) sign-off.

## Inputs

Awarded technical specification (binding), Stage 2 compliance matrix, confirmed OEM/vendor documents, detailed survey data.

## Calculations

Detailed link budget, cell planning, capacity/traffic dimensioning, power/battery autonomy, RAMS KPI substantiation — refining the Stage 2 tender-grade estimates with actual site and vendor data.

## Deliverables

- Technical specification (as-designed)
- Datasheet(s)
- Bill of Quantities
- System block diagram / drawings package
- Coverage study
- Detailed survey report
- Interface Control Documents
- RAMS/safety case
- Test and commissioning (FAT/SAT) plan
- Tools list / test-equipment requirements
- As-built documentation and O&M manuals (closing sub-phase, post-installation)

## Roles

- **Contractor** — primary producer of the full engineering package
- **PMC/Consultant** — review Contractor submittals for compliance against the Stage 2 spec
- **Client** — reviews/approves at contract-defined gates
- **Vendor/OEM** — supplies the technical documents the detailed design is built on
