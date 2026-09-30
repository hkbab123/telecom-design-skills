# Tender Stage — CCTV / Video Surveillance System

PMC + specialized CCTV/security-systems Consultant engaged by client, building the technical specification.

**Draft ordered decision sequence (public-standards-informed draft — needs correction from a practicing CCTV engineer):**

1. **Scope and coverage-zone definition** — the complete list of areas requiring coverage (rail: platforms, concourses, tunnels, depots/yards, train interiors; O&G: perimeter, process areas, access points), each with its purpose (deterrence, evidentiary, operational monitoring, process verification).
2. **Detection-vs-verification boundary** — explicitly state which functions are certified detection/alarm systems (intrusion detection, fire/gas detection, access control) and which are CCTV/VCA verification support — don't let this blur (rule 1).
3. **Hazardous-area zoning and equipment certification (O&G)** — classification drawing; every camera/housing/cable/junction box in a classified zone needs matching ATEX/IECEx certification. Gates equipment selection (item 9).
4. **System architecture** — centralised vs distributed VMS, number of monitoring/control-room locations, PSIM integration scope if any.
5. **Camera technology selection principles** — fixed vs PTZ vs fisheye-panoramic vs thermal, per coverage-zone purpose; minimum resolution/frame-rate/low-light (lux) performance targets.
6. **Video content analytics (VCA) requirements** — which zones get which analytics (motion, line-crossing, loitering, ANPR, PPE detection), and their operator-alert vs record-only status.
7. **Network architecture and segmentation** — dedicated CCTV/VMS VLAN, IT/OT boundary treatment, PoE power-budget approach.
8. **Cybersecurity and vendor-compliance requirements** — confirm early whether a banned-vendor-list restriction applies (rule 3); firmware/patch-management policy; VMS authentication/access-control requirements.
9. **Equipment dimensioning and selection basis** — camera/NVR/VMS-server/network-switch sizing (incl. which units need ATEX/IECEx per item 3).
10. **Bandwidth and storage sizing** — the calculated basis (camera count × resolution × fps × codec × retention), not an assumed figure (rule 4).
11. **Retention policy and data protection** — retention period (regulatory or client-driven), access-control and audit-trail requirements for recorded footage, data-protection/privacy compliance basis.
12. **Redundancy and availability targets** — VMS server redundancy, storage RAID/failover approach, network redundancy, stated per coverage-zone criticality.
13. **Interfaces** — grouped by family: **safety/detection systems** (item 2's boundary — intrusion/fire/gas detection); **PAGA** (CCTV-verified PA trigger); **SCADA** (video verification of process alarms); **access control**; **telecom systems** (network transport); **enterprise systems** (incident-management/evidence workflow).
14. **Regulatory approvals** — data-protection/privacy sign-off, any law-enforcement/evidentiary-chain-of-custody requirement (rail), process-safety interface approval (O&G).
15. **Compliance matrix** — map every requirement to IEC 62676, ONVIF profile conformance, IEC 60839, and the applicable data-protection regime.
16. **Tender-grade BOQ and testing/acceptance criteria** — BOQ basis; FAT/SAT criteria incl. coverage verification (does each zone actually achieve its stated purpose at the installed camera positions) and analytics false-alarm-rate testing.
17. **Verification & commissioning strategy** — pre-commissioning test approach, coverage walk-test methodology, cybersecurity configuration verification.

*(Harish: correct the order, flag anything missing or misplaced — same ask as the other subsystems' lists. Items 2 and 8 (detection/verification boundary; vendor-compliance) are where a practicing security-systems engineer's correction matters most, since they're the least like anything in GSM-R/TETRA/PAGA/SCADA.)*

- **Inputs:** Stage 1 outputs; PMC's oversight/format requirements; hazardous-area classification data (O&G); any banned-vendor-list restriction; data-protection regime applicable to the jurisdiction.
- **Decisions:** the 17-point sequence above.
- **Calculations:** camera-count finalisation per coverage zone; bandwidth/storage sizing (see `fundamentals/04-bandwidth-storage-calculations.md`); PoE power budget.
- **Deliverables:** CCTV technical specification (for tender), refined/accurate pricing data, Approved Vendor List (post any compliance-restriction filtering), compliance matrix.
- **Roles:** Consultant builds the spec and runs refined pricing; PMC oversees; Client owns the resulting tender; Contractor bids against it; Vendor/OEM/SI provides pricing, ends up on the AVL.

*(All figures above are illustrative — verify against the governing spec and applicable regulator for the specific project.)*
