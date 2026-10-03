# Engineering Stage — Transmission / Fibre Backbone

Contractor/SI-led detailed post-award design. Consultant/PMC review for compliance; OEM/Vendor supplies vendor-specific data.

**Draft ordered sequence (first-pass domain reconstruction, no project reference behind it yet):**

1. **Contract/spec kick-off** — confirm the awarded spec and Stage 2 compliance matrix; confirm hazardous-area zoning, route-diversity requirement and any vendor-compliance restriction as fixed inputs.
2. **Vendor/OEM document intake** — datasheets, optical-interface specifications, fibre and cable test certificates, ATEX/IECEx certificates where applicable. **OEM-sourcing rule applies here.**
3. **Detailed route survey** — as-found duct/trench/tray condition, joint-closure and node locations, crossings, third-party assets, permit constraints; for O&G, coordinate permit-to-work and confirm zoning against actual site conditions.
4. **Physical diversity verification** — walk each protected path pair on the survey data and record any shared structure (SRLG register); resolve or formally accept each exception with the client.
5. **Cable and fibre allocation plan** — fibre assignment per ring/segment/service, spare policy, ODF and patch-panel schedule, splice plan.
6. **Optical link-budget sheets** — per span: fibre length, attenuation, splice and connector counts, repair margin, dispersion check, transceiver or line-system reach confirmed from vendor documents.
7. **Technology-layer configuration design** — SDH/packet/OTN node configuration, VC or VLAN/service plan, protection groups, QoS or priority per service class.
8. **Synchronisation design** — reference source locations, distribution tree, holdover verification, SSM/clock-quality configuration.
9. **Network management design** — NMS server and DCN architecture, alarm mapping to the control room, performance-monitoring thresholds, OTDR monitoring if in scope.
10. **Cybersecurity detailed configuration** — management VLAN/DCN segmentation, role-based access, hardening baseline, firmware baseline, banned-vendor compliance on the actual selected equipment.
11. **Node-site power and environment design** — DC load per node, rectifier and battery sizing for autonomy, cooling/space per node room.
12. **Interface control documents (ICDs)** — one per interfacing subsystem (`fundamentals/16-interfacing-other-subsystems.md`), signed by the counterpart subsystem owner.
13. **Equipment dimensioning and final selection** — actual OEM part numbers, with certification applicability per unit/zone where relevant.
14. **Design documents and drawings** — block diagram, logical and physical topology drawings, route drawings, node layouts, cable and splice schedules.
15. **FAT plan** — protection-switch time, sync accuracy, service mapping, NMS alarm tests on factory equipment.
16. **Installation, splicing and fibre acceptance** — per-span OTDR and insertion-loss measurement against the link-budget sheets.
17. **SAT/commissioning plan** — end-to-end service activation, BER, protection tests including physical cut simulation on each protected path, sync verification, NMS integration.
18. **Handover and as-built** *(post-installation sub-phase)* — as-built route and splice records, final SRLG register, spares and maintenance manual.

*(Harish: first-pass reconstruction — please correct the order, flag gating dependencies, and sanity-check especially step 4 (diversity verification) and step 6 (budget sheets) once you're ready to share any project reference material.)*

**Document gating (starting points):**
- Route survey (step 3) gates diversity verification (step 4) and the cable allocation plan (step 5).
- Vendor documents (step 2) gate OEM-sourced figures in steps 6–13.
- Link-budget sheets (step 6) gate the technology-layer configuration (step 7) because line-system reach may change the node layout.
- ICDs (step 12) typically need the counterpart owner's countersignature before drawings (step 14) proceed.
- Fibre acceptance measurements (step 16) gate SAT (step 17).

- **Inputs:** awarded spec, Stage 2 compliance matrix, confirmed OEM/vendor documents, survey data, hazardous-area classification drawing (O&G).
- **Deliverables:** technical spec (as-designed), datasheets/certificates, BOQ, topology and route drawings, cable/splice/ODF schedules, link-budget sheets, sync plan, NMS design, ICDs, FAT/SAT plan, as-built documents and SRLG register.
- **Roles:** Contractor/SI produces the full package; PMC/Consultant review compliance; Client approves gates; Vendor/OEM supplies documents and certificates.
