# Tender Stage — FRMCS

PMC + specialised FRMCS Consultant engaged by the client, building the technical specification.

**Draft ordered decision sequence (public-standards-informed draft — needs correction by a practising FRMCS engineer):**

1. **Standards baseline** — pin the UIC FRMCS release, 3GPP release, ETSI/ERA documents and the version-control approach (Rule 4).
2. **Application and KPI matrix** — every application (critical, performance, business), owner, KPI (latency, reliability, throughput, priority), and the QoS class it maps to (Rule 1).
3. **Delivery model** — dedicated, hybrid or MNO-hosted/sliced; ownership and operating responsibilities; SLA structure (Rule 2).
4. **Spectrum and coexistence** — bands, bandwidth, duplex mode, neighbouring services, guard bands, regulatory approvals (Rule 5).
5. **Coverage requirement and RF design basis** — coverage targets per application, propagation model, link-budget basis, site-spacing assumption, tunnel/station/viaduct treatment.
6. **Capacity dimensioning** — demand per cell for the worst scenario (trains per cell, video, data), headroom, QoS protection of critical traffic.
7. **Mobility and handover requirement** — maximum speed, interruption-time target, cell overlap policy, behaviour across network boundaries.
8. **Core and service platform** — core generation (5G core / EPC), mission-critical service servers, IMS, slicing, user-plane/edge placement, multi-vendor interfaces.
9. **Transition and coexistence** — overlay/migration requirements, interworking, dual-mode on-board, ordering of cutover (Rule 3).
10. **On-board architecture** — gateway, antennas, bearers, SIM/credential strategy, cab interface, fleet retrofit scope (Rule 8).
11. **Safety communication boundary** — ETCS/ATO data requirements, EN 50159 considerations, who owns what in the safety case (Rule 6).
12. **Backhaul and synchronisation** — transport capacity and latency, TDD phase synchronisation source, dependency on the transmission and master-clock subsystems.
13. **Redundancy and availability targets** — core geo-redundancy, RAN overlap, backhaul diversity, per-application availability.
14. **Cybersecurity** — identity, SIM/eSIM lifecycle, network zones and conduits, management-plane security, logging (Rule 7).
15. **Network management and KPI monitoring** — OSS scope, KPI measurement method, on-board measurement, alarm integration to the control centre.
16. **Interfaces** — grouped by family: **signalling** (ETCS, ATO, interlocking), **dispatcher and control centre**, **transport** (transmission), **timing** (master clock), **security/video** (CCTV), **passenger information**, **legacy radio** (GSM-R, TETRA), **public-network and roaming**.
17. **Regulatory and cross-border approvals** — licences, interconnect and roaming agreements, type approval, interoperability certification.
18. **Vendor and component compliance** — banned-vendor-list check, sovereign-sourcing rules (Rule 9).
19. **Compliance matrix** — map each requirement to UIC, 3GPP, ETSI, CEPT and CENELEC references (`standards.md`).
20. **Tender-grade BOQ, acceptance criteria and verification strategy** — BOQ basis; acceptance tests (coverage and KPI measurement, handover, interoperability, failover, security); test sequence and witnessing.

*(Harish: correct the order, flag anything missing or misplaced — same ask as the other subsystems. Items 2 and 3 (application/KPI matrix and delivery model) are the ones I'd most like a practising FRMCS engineer to check.)*

- **Inputs:** Stage 1 outputs; PMC's oversight/format requirements; spectrum position; fleet inventory; any banned-vendor restriction; client network-architecture standards.
- **Decisions:** the 20-point sequence above; coverage and capacity refined from parametric to specification-grade.
- **Deliverables:** technical specification, application/KPI matrix, delivery-model definition, compliance matrix, tender BOQ, acceptance criteria, ICD requirement list.
- **Roles:** Consultant authors; PMC reviews; Client approves; Vendor/OEM supplies indicative data under the OEM-sourcing rule.
