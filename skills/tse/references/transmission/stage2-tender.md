# Tender Stage — Transmission / Fibre Backbone

PMC + specialised transmission Consultant engaged by the client, building the technical specification.

**Draft ordered decision sequence (public-standards-informed draft — needs correction by a practising transmission engineer):**

1. **Service catalogue and owners** — every subsystem that rides on the transport (GSM-R/TETRA backhaul, SCADA, CCTV, PAGA, PABX, master clock, enterprise/IT), with owner, interface type (E1, Ethernet, serial) and criticality class per service.
2. **Topology and physical-route diversity requirement** — ring/mesh/linear structure, and an explicit requirement that protected paths are physically separate (no shared duct/trench/bridge/cross-passage) with SRLG identification (Rule 1).
3. **Technology decision and migration** — SDH/NG-SDH vs packet transport (MPLS-TP/Carrier Ethernet) vs OTN/DWDM, driven by the service catalogue and Q1b, including circuit emulation or phased migration for legacy TDM (Rule 4).
4. **Fibre cable specification** — fibre type, fibre count with spare, cable construction per environment (tunnel, viaduct, direct-buried, duct, aerial, pipeline corridor), fire/smoke/halogen performance.
5. **Route and civil interface** — duct/trench/cable-tray provisions, separate routes where Rule 1 requires, joint-closure locations, cross-passage and bridge crossings, third-party asset crossings.
6. **Capacity dimensioning and growth margin** — aggregate per segment from the service matrix, with stated growth horizon and headroom.
7. **Optical link-budget basis and node spacing** — budget method, end-of-life margin policy (Rule 3), amplifier/regenerator placement where spans exceed reach.
8. **Protection and restoration scheme** — protection type per service class, switch-time target, behaviour on multiple failures.
9. **Synchronisation architecture** — reference sources, distribution plan, holdover requirement (Rule 5).
10. **Hazardous-area and offshore provisions (O&G)** — zoning drawing, optical-power limits in classified areas, subsea/offshore cable and landing requirements (`fundamentals/11-og-pipeline-plant-offshore-fibre.md`).
11. **Network management and OAM scope** — NMS architecture, alarm integration to the control room, performance monitoring, OTDR-based fibre monitoring if required.
12. **Node-site power and environment** — DC supply, battery autonomy, cooling and space per node type.
13. **Cybersecurity and vendor compliance** — management-plane segmentation, access control, encryption requirements, banned-vendor-list check (Rule 6).
14. **Availability and RAMS targets** — per service class, with MTTR assumptions for cable repair and spares strategy.
15. **Interfaces** — grouped by family: **radio systems** (GSM-R, TETRA), **control systems** (SCADA), **security/video** (CCTV), **voice and alarm** (PAGA, PABX), **timing** (master clock), **enterprise/IT**.
16. **Regulatory and right-of-way approvals** — route permits, authority crossings, spectrum/licensing where any optical-wireless link is included.
17. **Compliance matrix** — map each requirement to ITU-T, IEC and IEEE references (`standards.md`).
18. **Tender-grade BOQ and acceptance criteria** — BOQ basis; acceptance tests (fibre loss/OTDR, BER, service activation, protection-switch time, sync accuracy).
19. **Verification and commissioning strategy** — test sequence, who witnesses, how multi-route diversity is physically verified on site.

*(Harish: correct the order, flag anything missing or misplaced — same ask as the other subsystems. Items 2 and 7 (diversity and end-of-life budget) are the ones I'd most like a practising transmission engineer to check.)*

- **Inputs:** Stage 1 outputs; PMC's oversight/format requirements; hazardous-area data (O&G); any banned-vendor restriction; client network-architecture standards.
- **Decisions:** the 19-point sequence above; capacity and link budgets refined from parametric to specification-grade.
- **Deliverables:** technical specification, service matrix, route/diversity requirement, compliance matrix, tender BOQ, acceptance criteria, ICD requirement list.
- **Roles:** Consultant authors; PMC reviews; Client approves; Vendor/OEM supplies indicative data under the OEM-sourcing rule.
