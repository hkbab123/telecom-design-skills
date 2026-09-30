# Engineering Stage — CCTV / Video Surveillance System

Contract awarded to the Contractor/System Integrator; Stage 2 spec becomes the binding contract requirement; Consultant/PMC shift to review/compliance role; OEM/Vendor supplies vendor-specific technical documents.

**Draft ordered sequence:**

1. **Contract/spec kick-off and compliance baseline** — review awarded spec and Stage 2 compliance matrix; confirm hazardous-area zoning and any vendor-compliance restriction as fixed inputs.
2. **Vendor/OEM confirmation and vendor document intake** — datasheets, ATEX/IECEx certificates, ONVIF conformance statements. **OEM-sourcing rule applies from here.**
3. **Detailed site survey** — camera-position survey per coverage zone, mounting-structure availability, cable-routing, power availability (PoE reach limits); for O&G, coordinate with permit-to-work and confirm hazardous-area classification against actual site conditions.
4. **Coverage design and camera schedule finalisation** — exact camera position, orientation, lens/field-of-view, and technology per position, verified against the Stage 2 coverage-zone purpose (does this position actually achieve deterrence/evidentiary/operational intent).
5. **VCA configuration design** — per-camera analytics configuration (motion/line-crossing/loitering/ANPR/PPE), detection zones, sensitivity, and expected false-alarm-rate mitigation.
6. **Network architecture and segmentation detailed design** — VLAN/subnet plan, IT/OT boundary implementation, PoE switch/budget finalisation per site.
7. **Cybersecurity detailed configuration** — firmware baseline, patch-management process, VMS authentication/role-based access control, banned-vendor-list compliance verification per actual selected equipment.
8. **Storage architecture detailed design** — NVR/VMS-server sizing, RAID configuration, retention-period implementation against the calculated bandwidth/storage basis.
9. **Redundancy implementation** — VMS server/storage failover, network redundancy against real site topology.
10. **Equipment dimensioning and selection (final)** — actual OEM part numbers (confirming ATEX/IECEx applicability per unit/zone).
11. **Power system design per site** — PoE budget per switch, UPS/battery autonomy for VMS server/core network equipment.
12. **VMS/PSIM configuration design** — control-room layout, video-wall/workstation allocation, PSIM integration configuration if in scope.
13. **Interface Control Documents (ICDs)** — one per interface family; the detection-system boundary ICD (item 2 of Stage 2) and any evidentiary chain-of-custody workflow are the most scrutiny-worthy of these.
14. **Data-protection and retention implementation** — access-control/audit-trail configuration, retention-period enforcement, privacy-masking configuration where required.
15. **System block diagrams and drawings package** — architecture/network diagram (IT/OT boundary marked), camera-location drawings, cable schedules, hazardous-area overlay (O&G).
16. **Technical specification (as-designed) and datasheet/certificate compilation.**
17. **Bill of Quantities (final).**
18. **Test and commissioning plan (FAT/SAT)** — per-camera image-quality and coverage verification, VCA false-alarm-rate testing, cybersecurity configuration verification, redundancy/failover testing, retention-policy verification.
19. **As-built documentation and O&M handover** *(post-installation closing sub-phase)* — as-built drawings, O&M manuals, training records, spares list, hazardous-area equipment certificate register.

*(Harish: first-pass domain reconstruction, no project reference behind it yet — please correct order, flag gating dependencies, and sanity-check especially steps 4-5 (coverage/VCA design) and step 7 (cybersecurity compliance) once you're ready to share any project reference material.)*

**Document gating (starting points):**
- Hazardous-area zoning confirmation (step 1) gates equipment selection (step 10) and installation design for O&G sites.
- Vendor documents (step 2) gate every OEM-sourced figure in steps 8-18.
- Coverage design/camera schedule (step 4) gates VCA configuration (step 5) — analytics can't be configured against a position that hasn't been finalised.
- Network architecture (step 6) typically needs Client/PMC IT-security sign-off before commissioning (step 18).
- ICDs (step 13) typically need the other system's owner (fire/gas detection, PAGA, SCADA, access control) to countersign before drawings (step 15) proceed.

- **Inputs:** awarded spec, Stage 2 compliance matrix, confirmed OEM/vendor documents, detailed survey data, hazardous-area classification drawing (O&G), applicable data-protection regime.
- **Deliverables:** technical spec (as-designed), datasheets/certificates, BOQ, block diagram/drawings incl. network (IT/OT) and hazardous-area overlays, camera schedule, VCA configuration design, detailed survey report, ICDs, FAT/SAT plan, as-built docs + certificate register.
- **Roles:** Contractor/SI produces the full package; PMC/Consultant review for compliance; Client approves at gates; Vendor/OEM supplies documents/certificates.
