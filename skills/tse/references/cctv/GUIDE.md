CCTV (Closed-Circuit Television) / IP Video Surveillance System (VSS) is the video monitoring, recording, and analytics subsystem used for security, safety-evidentiary, and operational-monitoring purposes on rail projects (station/platform/tunnel surveillance, train-borne CCTV, Video Recording Systems (VRS)) and oil & gas projects (plant/field perimeter security, hazardous-area process monitoring, thermal/early-fire detection support).

**Content basis:** built from public IP-video-surveillance standards knowledge (IEC 62676 series, ONVIF profiles, IEC 60839) and general VSS design practice, not from a specific past project. Treat its decision sequences as a solid, standards-grounded starting point that still benefits from correction by a practicing CCTV/security-systems engineer — see `CONTRIBUTING.md` in the repo root. Harish may supply project-specific reference material later as a gap-fill round, same pattern as SCADA.

## Subsystem-specific rules (in addition to the umbrella design rules)

1. **CCTV verifies, it does not detect.** A video-content-analytics (VCA) alert — motion, line-crossing, loitering — is an aid to an operator or a supporting input to a separate certified detection/alarm system (intrusion detection, fire/gas detection). Never spec CCTV/VCA as a substitute for a certified detection system unless the specific analytics function is itself independently certified for that purpose.
2. **Hazardous-area certification is not optional for O&G.** Any camera, housing, cable gland, or junction box sited in a classified hazardous area needs matching ATEX/IECEx certification — flag this at Concept, not at procurement.
3. **Vendor/component cybersecurity compliance is a spec-stage gate.** Many rail and government-adjacent projects exclude specific camera/VMS manufacturers by name on national-security grounds (banned-vendor lists). Confirm this requirement at Tender stage, before any OEM shortlist is built — discovering it at Engineering stage is expensive to unwind.
4. **Bandwidth and storage sizing must be calculated, not assumed.** Camera count × resolution × frame rate × codec efficiency × retention period drives both the network and storage architecture — never state an NVR/storage figure without showing the calculation (see `fundamentals/04-bandwidth-storage-calculations.md`).

## Step 1 — Confirm stage, deployment context, and role

**Q1 — What stage is the project at?**
- **Concept** → `stage1-concept.md`
- **Tender** → `stage2-tender.md`
- **Engineering** → `stage3-engineering.md`

**Q1b — Deployment context, and is any part of it in a classified hazardous area?**
- **Rail** — station/platform surveillance, tunnel CCTV, train-borne CCTV/VRS, depot/yard ANPR.
- **Oil & gas** — plant/perimeter security surveillance, process-area monitoring, thermal/flare-stack surveillance. If any camera sits in a classified zone, ATEX/IECEx certification is a hard constraint from here on (rule 2).

**Q2 — Who are you representing?**
Same five roles as the other subsystems: **Client**, **PMC**, **Specialized Consultant**, **Contractor**, **Vendor/OEM/System Integrator**.

## Step 2 — Work the stage-specific sequence

Read the matching stage file and walk the user through it as an ordered sequence of decisions, checked against the governing standards (`standards.md`), any stated client requirement, hazardous-area zoning where flagged, and the outputs of the previous stage.

**When a question is conceptual, not sequential** (e.g. "why does ONVIF matter," "how do I size storage," "what's the difference between a detection alarm and a VCA alert") — pull from the matching `fundamentals/` file rather than answering from general knowledge; the reasoning and worked examples live there.

## Step 3 — Produce the deliverable

Match detail to stage: Concept is order-of-magnitude/parametric (camera counts, coverage zones), Tender is specification-grade (technical spec, compliance matrix, bandwidth/storage calculation basis), Engineering is detailed and vendor-sourced (camera schedule, network diagram, storage BOQ, FAT/SAT plan).

## Reference files

- `stage1-concept.md` — Concept stage: feasibility, camera-count/coverage-zone estimation, stakeholder requirements, market RFI
- `stage2-tender.md` — Tender stage: the technical specification decision sequence
- `stage3-engineering.md` — Engineering stage: the detailed post-award design sequence
- `standards.md` — Standards this skill references (IEC 62676, ONVIF, IEC 60839, ATEX/IECEx) and what each governs

## Technical fundamentals (`fundamentals/`)

1. `01-video-surveillance-architecture.md` — IEC 62676 system architecture, camera/network/VMS/storage layers, centralised vs distributed VMS, PSIM integration.
2. `02-camera-technology-selection.md` — fixed/PTZ/fisheye-panoramic/thermal/Ex-rated camera types, lux/IR performance, lens selection basics.
3. `03-ip-video-protocols-onvif.md` — ONVIF profiles (S/T/G/Q), RTSP/RTP streaming, H.264/H.265 codec basics.
4. `04-bandwidth-storage-calculations.md` — worked bitrate and storage-sizing calculation (resolution × fps × compression × retention × camera count).
5. `05-network-design-for-cctv.md` — dedicated VLAN, multicast for live viewing, QoS, PoE power budgeting.
6. `06-video-content-analytics.md` — VCA types (motion, line-crossing, loitering, ANPR, PPE detection), false-alarm-rate management.
7. `07-cctv-as-verification-not-detection.md` — the core distinction: CCTV's verification role vs a certified detection/alarm system's role — technical basis for Subsystem-specific rule 1.
8. `08-hazardous-area-camera-certification.md` — ATEX/IECEx Ex-rated camera housings and cabling for O&G — technical basis for Subsystem-specific rule 2.
9. `09-rail-station-platform-tunnel-cctv.md` — platform/tunnel-specific design constraints (EMC from traction power, vibration, low-light), passenger safety/evidentiary role.
10. `10-train-borne-cctv-vrs.md` — train-borne CCTV, VRS (Video Recording System) terminology, driver's forward-facing camera, onboard-to-trackside wireless offload.
11. `11-og-perimeter-thermal-surveillance.md` — O&G perimeter security design, thermal imaging for early fire/flare-stack surveillance, PIDS integration.
12. `12-cybersecurity-vendor-compliance.md` — banned-vendor-list compliance, IT/OT segmentation for the VMS network (ties to SCADA's IEC 62443 discipline), firmware/patch management.
13. `13-privacy-data-protection-retention.md` — data-protection/privacy principles, footage retention policy, access-control and audit trail for recorded footage.
14. `14-integration-with-other-systems.md` — PSIM, interfaces with access control/PIDS, PAGA (CCTV-verified PA trigger), SCADA (video verification of process alarms), ICD requirements.

## Status

CCTV was added 30-Sep-26 as the fifth built subsystem, from public standards knowledge (v0.1, pending a gap-fill round against Harish's own project reference material, same pattern as SCADA).
