# FRMCS — Subsystem Guide

Future Railway Mobile Communication System: the successor to GSM-R, a bearer-agnostic, all-IP railway communication platform built on 3GPP mission-critical services over 5G NR (with LTE as an early bearer). It carries railway critical communications (voice and group calls, train control data such as ETCS and ATO), performance applications (e.g. train-to-ground video, remote diagnostics) and business applications (e.g. passenger and operational data), through trackside radio, a core and service platform, backhaul, and an on-board gateway.

**Rail only.** FRMCS has no oil & gas variant; this subsystem covers mainline, high-speed, regional and urban/metro railways. It is **independent** of the GSM-R subsystem: you can run a full FRMCS design session without loading anything from `references/gsmr/`. Where a project spans both (an overlay or migration), work each sequence separately and use `fundamentals/13-gsmr-coexistence-and-migration.md` for the boundary.

**Content basis:** built from public UIC, 3GPP, ETSI, CEPT/ECC and CENELEC standards knowledge and general mission-critical mobile-network design practice, not from a specific past project. No OEM-proprietary documentation (Nokia, Huawei, Ericsson, Siemens, Alstom, Hitachi or any other vendor) is used. FRMCS standardisation is still moving, so every project must pin the specification baseline (see Rule 4). Treat its decision sequences as a standards-grounded starting point that still benefits from correction by a practising FRMCS/mission-critical-network engineer — see `CONTRIBUTING.md` in repo root. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA and CCTV.

## Subsystem-specific rules (in addition to umbrella design rules)

1. **Application-first and bearer-agnostic.** Design from the FRMCS application categories (critical, performance, business) and their KPIs, not from the radio technology. Radio, core, backhaul and on-board gateway are chosen to meet the application KPIs. See `fundamentals/02-application-categories-qos-kpis.md`.
2. **Delivery model is the first architectural fork.** A dedicated railway network, a hybrid with public-network support, and an MNO-hosted or sliced service are different designs with different risk, cost and control. GSM-R's assumption that the railway owns the whole radio network no longer holds by default. See `fundamentals/10-delivery-models-private-hybrid-mno.md`.
3. **Coexistence and migration are design inputs, not a later phase.** Existing GSM-R, mixed fleets and dual-mode on-board equipment shape the architecture from Concept stage. See `fundamentals/13-gsmr-coexistence-and-migration.md`.
4. **Pin the standards baseline.** The UIC FRMCS specification set, 3GPP releases and ETSI/ERA documents are still evolving. State the baseline version in every deliverable, check its current status against the source, and treat anything in this folder as a pointer, not a definitive statement. See `fundamentals/20-standards-maturity-and-version-control.md`.
5. **Frequency changes the radio design.** FRMCS bands sit differently from GSM-R's, and a higher-frequency carrier needs more sites for the same corridor. Do not assume existing GSM-R sites reproduce the coverage. See `fundamentals/06-coverage-link-budget-and-site-planning.md`.
6. **FRMCS carries safety communication but is not the safety system.** Train-control data (ETCS, ATO) uses FRMCS as a transmission path whose properties feed the signalling safety case (EN 50159 / EN 50126 / EN 50129). Specify the communication requirements, not the signalling logic. See `fundamentals/12-etcs-ato-and-safety-communication.md`.
7. **Cybersecurity is first-class.** An all-IP, standards-based, multi-tenant platform has an IT-style attack surface. Identity, SIM/credential lifecycle and zone/conduit design are specified from Tender stage. See `fundamentals/16-security-identity-sim-key-management.md`.
8. **On-board equipment is in scope.** The gateway, antennas, bearers and cab interface determine whether the application KPIs are met. See `fundamentals/11-onboard-gateway-multi-bearer.md`.
9. **Vendor/component compliance is a spec-stage gate.** Same rule as CCTV and Transmission: confirm any banned-vendor-list or sovereign-sourcing restriction at Tender stage, before an OEM shortlist is built.

## Step 1 — Intake questions

**Q1 — Which stage?** Concept, Tender or Engineering (reads `stage1-concept.md` / `stage2-tender.md` / `stage3-engineering.md`).

**Q1b — Which situation?**
- **Greenfield FRMCS** (new line or network with no existing mobile radio)
- **Overlay** on an existing GSM-R network (both run in parallel)
- **Migration** of an existing GSM-R network to FRMCS with a defined cutover plan

This gates how much of `13-gsmr-coexistence-and-migration.md` applies.

**Q1c — What is the delivery model?** Dedicated railway network, hybrid (railway network plus public-network support), or MNO-hosted/sliced service; or "not decided". If not decided, Concept stage must present options (rule 2).

**Q1d — Is spectrum allocated?** Which band(s), how much, and to whom (railway, MNO, shared). This gates the radio design and coexistence work (`fundamentals/05`).

**Q1e — Does the line cross a border or run through shared infrastructure?** Cross-border roaming and interconnect, and tunnels or stations shared with other operators, change the core and coverage design.

**Q2 — Who are you representing?** Same five roles as other subsystems: **Client** (infrastructure manager or railway operator), **PMC**, **Specialized Consultant**, **Contractor**, **Vendor/OEM/System Integrator**.

## Step 2 — Work the stage-specific sequence

Read the matching stage file and walk the user through the ordered decisions, checked against governing standards (`standards.md`), any stated client requirement, and outputs of the previous stage.

**When the question is conceptual, not sequential** (e.g. "how does MCPTT replace group calls", "why does 1.9 GHz need more sites", "what does the on-board gateway do") — pull the matching `fundamentals/` file rather than answering from general knowledge; the reasoning and worked examples live there.

## Step 3 — Produce the deliverable

Match detail to the stage: Concept is order-of-magnitude (application list, delivery-model options, site-count range, transition strategy), Tender is specification-grade (technical specification, application/KPI matrix, compliance matrix, interface list), Engineering is detailed and vendor-sourced (RF design, core and service design, on-board design, QoS/slice configuration, security design, FAT/SAT and migration plan).

## Reference files

- `stage1-concept.md` — Concept stage: feasibility, transition strategy, delivery-model options, market RFI
- `stage2-tender.md` — Tender stage: 20-point technical specification decision sequence
- `stage3-engineering.md` — Engineering stage: 20-step detailed post-award design sequence
- `standards.md` — Standards this skill references (UIC FRMCS set, 3GPP, ETSI, CEPT/ECC, CENELEC, IEC 62443)

### Fundamentals (conceptual deep-dives)

1. `01-frmcs-concept-and-architecture-layers.md` — application, service and transport layers, how FRMCS sits on 3GPP mission-critical services.
2. `02-application-categories-qos-kpis.md` — critical/performance/business categories, 5QI mapping, KPIs — basis for Rule 1.
3. `03-mission-critical-services-mcptt-mcdata-mcvideo.md` — MCPTT/MCData/MCVideo, functional identity, priority and pre-emption; GSM-R-to-FRMCS service mapping.
4. `04-5g-nr-lte-radio-for-rail.md` — NR/LTE basics for railway use: duplex modes, bandwidth, MIMO, Doppler worked example.
5. `05-spectrum-and-coexistence.md` — FRMCS bands, neighbours, guard bands, regulatory check — basis for Rule 5.
6. `06-coverage-link-budget-and-site-planning.md` — path-loss/frequency worked example, site reuse, tunnels and stations — basis for Rule 5.
7. `07-capacity-dimensioning.md` — per-cell demand versus capacity worked example, QoS protection of critical traffic.
8. `08-mobility-handover-high-speed.md` — handover at speed, interruption time, Doppler, overlap planning.
9. `09-core-network-and-service-platform.md` — 5G core / EPC, MC service servers, IMS, slicing, edge placement.
10. `10-delivery-models-private-hybrid-mno.md` — dedicated vs hybrid vs MNO-hosted/sliced — basis for Rule 2.
11. `11-onboard-gateway-multi-bearer.md` — on-board gateway, multi-bearer selection, cab and antenna design — basis for Rule 8.
12. `12-etcs-ato-and-safety-communication.md` — ETCS/ATO data over FRMCS, EN 50159, safety-case boundary — basis for Rule 6.
13. `13-gsmr-coexistence-and-migration.md` — overlay, interworking, dual-mode on-board, cutover — basis for Rule 3.
14. `14-backhaul-transport-synchronisation.md` — fibre backhaul, TDD phase synchronisation, link to the transmission and master-clock subsystems.
15. `15-redundancy-resilience-availability.md` — core and RAN redundancy, overlapping coverage, failure modes.
16. `16-security-identity-sim-key-management.md` — 3GPP and MC security, SIM/eSIM lifecycle, zones and conduits — basis for Rule 7.
17. `17-network-management-monitoring-kpi.md` — OSS, KPI monitoring, QoS measurement, alarming.
18. `18-interfacing-other-subsystems.md` — ICD requirements with signalling, transmission, master clock, SCADA, CCTV, PIS, PAGA and legacy radio.
19. `19-testing-commissioning-certification.md` — lab interoperability, field trials, drive/ride testing, regression across releases.
20. `20-standards-maturity-and-version-control.md` — baselines, release tracking, change control — basis for Rule 4.

## Status

FRMCS was added 11-Oct-26 as the eighth built subsystem, from public standards knowledge (v0.1, pending a gap-fill round against Harish's own project reference material). It was built as an independent subsystem at Harish's instruction, not as a variant inside the GSM-R folder.
