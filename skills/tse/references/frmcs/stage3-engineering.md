# Engineering Stage — FRMCS

Contractor/SI-led detailed post-award design. Consultant/PMC review for compliance; OEM/Vendor supplies vendor-specific data.

**Draft ordered sequence (first-pass domain reconstruction, no project reference behind it yet):**

1. **Contract/spec kick-off** — confirm the awarded spec, the pinned standards baseline and the Stage 2 compliance matrix; confirm delivery model, spectrum and any vendor-compliance restriction as fixed inputs.
2. **Vendor/OEM document intake** — datasheets, conformance and interoperability certificates against the baseline, on-board gateway and antenna specifications, security certifications. **OEM-sourcing rule applies here.**
3. **Application and KPI confirmation** — confirm each application's real traffic profile and KPI with its owner (signalling, operations, CCTV, maintenance); update the KPI matrix.
4. **Site and route survey** — existing towers, shelters, power, fibre; tunnels, stations, viaducts, cuttings; shadowing and interference sources; coexistence with neighbouring services.
5. **RF design** — propagation model calibration, site positions, antenna types and heights, cell overlap for handover, tunnel and station coverage design, link-budget sheets (`fundamentals/06`).
6. **Capacity design** — per-cell demand, carrier configuration, QoS and priority plan, slice or QoS-class configuration (`fundamentals/07`).
7. **Mobility design** — handover parameters, neighbour relations, overlap lengths, behaviour at network and tunnel boundaries (`fundamentals/08`).
8. **Core and service design** — core deployment, MC service servers, IMS, identity and addressing plan, user-plane/edge placement, geo-redundancy (`fundamentals/09`, `15`).
9. **Backhaul and synchronisation design** — transport capacity and latency per site, phase-synchronisation source and distribution, protection (`fundamentals/14`).
10. **On-board design** — gateway configuration, bearer-selection policy, antenna placement, cab interface, retrofit installation plan per fleet (`fundamentals/11`).
11. **Safety communication design** — ETCS/ATO data path, QoS for safety-related flows, EN 50159 measures agreed with the signalling contractor (`fundamentals/12`).
12. **Coexistence and migration design** — interworking function, dual-mode handling, cutover sequence, fallback and rollback plan (`fundamentals/13`).
13. **Cybersecurity detailed configuration** — SIM/eSIM provisioning, key management, authentication, network zones, hardening baseline, logging, banned-vendor compliance on the actual selected equipment (`fundamentals/16`).
14. **Network management design** — OSS architecture, KPI collection including on-board measurement, alarm mapping to the control centre (`fundamentals/17`).
15. **Interface control documents (ICDs)** — one per interfacing subsystem (`fundamentals/18`), signed by the counterpart subsystem owner.
16. **Equipment dimensioning and final selection** — actual OEM part numbers, with certification applicability per unit.
17. **Design documents and drawings** — architecture and logical diagrams, site layouts, RF plots, core and IP plans, on-board installation drawings.
18. **FAT and lab interoperability plan** — conformance and interoperability tests on factory equipment against the pinned baseline (`fundamentals/19`).
19. **Installation, field trials and drive/ride testing** — coverage and KPI measurement against the design, handover tests at speed, tunnel and station tests, on-board measurements.
20. **SAT, migration execution and handover** — end-to-end application tests with the signalling and control systems, security tests, cutover and rollback rehearsal, as-built, spares, and maintenance and release-management manual.

*(Harish: first-pass reconstruction — please correct the order, flag gating dependencies, and sanity-check especially step 3 (KPI confirmation) and step 12 (coexistence and migration design) once you're ready to share any project reference material.)*

**Document gating (starting points):**
- KPI confirmation (step 3) gates RF, capacity and core design (steps 5–8).
- Site and route survey (step 4) gates RF design (step 5) and backhaul (step 9).
- Vendor documents and the pinned baseline (step 2) gate OEM-sourced figures in steps 5–16.
- Safety communication design (step 11) must be agreed with the signalling contractor before the ICD (step 15) is signed.
- ICDs (step 15) typically need counterpart countersignature before drawings (step 17) proceed.
- Lab interoperability (step 18) gates field installation of on-board equipment (step 19).

- **Inputs:** awarded spec, Stage 2 compliance matrix, pinned baseline, confirmed OEM/vendor documents, survey data, fleet inventory, spectrum licence terms.
- **Deliverables:** technical spec (as-designed), datasheets/certificates, BOQ, RF design and link-budget sheets, capacity and QoS plan, core and IP plans, on-board design, security design, migration plan, ICDs, FAT/SAT and field-trial plans, as-built documents.
- **Roles:** Contractor/SI produces the full package; PMC/Consultant review compliance; Client approves gates; Vendor/OEM supplies documents and certificates.
