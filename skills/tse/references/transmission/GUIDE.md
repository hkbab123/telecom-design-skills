# Transmission / Fibre Backbone — Subsystem Guide

Optical fibre and transmission-network subsystem (SDH/NG-SDH, packet transport, OTN/DWDM) that carries the traffic of every other telecom and control subsystem on rail projects (trackside/tunnel fibre backbone, station and depot rings) and oil & gas projects (plant rings, pipeline-corridor backbone, field-to-control-centre links, offshore links).

**Content basis:** built from public ITU-T, IEC and IEEE standards knowledge and general transport-network design practice, not from a specific past project. No OEM-proprietary documentation (Huawei, Nokia, Ciena, Cisco or any other vendor) is used. Treat its decision sequences as a standards-grounded starting point that still benefits from correction by a practising transmission engineer — see `CONTRIBUTING.md` in repo root. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA and CCTV.

## Subsystem-specific rules (in addition to umbrella design rules)

1. **Physical diversity is not logical diversity.** A ring or dual-homed topology that looks protected on a logical diagram can share one duct, trench, bridge, cross-passage or cable tray, so a single cut takes out both paths. Every protection claim must be checked against the physical route and its shared-risk link groups (SRLG). See `fundamentals/07-protection-restoration-physical-diversity.md`.
2. **Transport is the shared dependency of every other subsystem.** GSM-R, TETRA, SCADA, CCTV, PAGA and PABX all inherit this subsystem's availability. Design per service class (isolation, priority, protection level per client subsystem), not just aggregate capacity. See `fundamentals/09-capacity-dimensioning-service-mapping.md`.
3. **Link budgets are computed at end-of-life, not day one.** Include repair splices, connector ageing, bend and temperature effects, and an operating margin. See `fundamentals/03-optical-link-budget-dispersion.md`.
4. **Legacy TDM presence decides the technology.** If any connected subsystem still needs E1/STM-n handoff (e.g. legacy radio base-station links, legacy PABX trunks), the transport cannot be a pure packet network without circuit emulation or a migration plan. Ask this at intake (Q1b).
5. **Timing is part of transport's job.** Frequency (and, where needed, phase) synchronisation for TDM-based radio and other timing-sensitive services is delivered by the transport network. A transport design without a synchronisation architecture is incomplete. See `fundamentals/08-synchronization-timing.md`.
6. **Vendor/component compliance is a spec-stage gate.** Same rule as CCTV: confirm any banned-vendor-list or sovereign-sourcing restriction at Tender stage, before an OEM shortlist is built.

## Step 1 — Intake questions

**Q1 — Which domain?**
- **Rail** — trackside/tunnel fibre backbone, station and depot rings, control-centre (OCC/BCC) connectivity.
- **Oil & gas** — plant/terminal rings, pipeline-corridor backbone, field-to-control-room links, offshore/subsea links.

**Q1b — Which services must the transport carry, and is any of it legacy TDM?** (E1, STM-n, serial/RS-232 or RS-485 tails vs all Ethernet/IP.) This gates technology choice (rule 4) and whether circuit emulation or a phased migration is in scope.

**Q1c — Is any route in a classified hazardous area, or offshore/subsea?** If so, `fundamentals/11-og-pipeline-plant-offshore-fibre.md` applies from the first stage.

**Q2 — Who are you representing?** Same five roles as other subsystems: **Client**, **PMC**, **Specialized Consultant**, **Contractor**, **Vendor/OEM/System Integrator**.

## Step 2 — Work the stage-specific sequence

Read the matching stage file and walk the user through the ordered decisions, checked against governing standards (`standards.md`), any stated client requirement, and outputs of the previous stage.

**When the question is conceptual, not sequential** (e.g. "why does SRLG matter", "how do I compute an optical budget", "SDH versus MPLS-TP") — pull the matching `fundamentals/` file rather than answering from general knowledge; the reasoning and worked examples live there.

## Step 3 — Produce the deliverable

Match detail to the stage: Concept is order-of-magnitude (route length, node count, fibre count, technology direction), Tender is specification-grade (technical spec, compliance matrix, service matrix, link-budget basis), Engineering is detailed and vendor-sourced (cable schedule, splice and ODF plan, link-budget sheets, node configuration, sync plan, FAT/SAT plan).

## Reference files

- `stage1-concept.md` — Concept stage: feasibility, route/node/capacity estimation, stakeholder requirements, market RFI
- `stage2-tender.md` — Tender stage: technical specification decision sequence
- `stage3-engineering.md` — Engineering stage: detailed post-award design sequence
- `standards.md` — Standards this skill references (ITU-T G-series, IEC 60793/60794, IEEE 1588, MEF, IEC 62443)

### Fundamentals (conceptual deep-dives)

1. `01-transport-network-architecture-layers.md` — layering (fibre, optical, TDM/OTN, packet, service), access/aggregation/core roles, where each subsystem plugs in.
2. `02-optical-fibre-types-cable-construction.md` — G.652/G.655/G.657, single-mode vs multimode, cable constructions, fire/smoke/halogen performance.
3. `03-optical-link-budget-dispersion.md` — loss budget, margin, chromatic/polarisation-mode dispersion, OSNR — technical basis for Rule 3.
4. `04-sdh-ng-sdh-fundamentals.md` — SDH hierarchy, VC containers, MSP/SNCP, GFP/VCAT/LCAS for Ethernet over SDH.
5. `05-packet-transport-mpls-tp-carrier-ethernet.md` — Carrier Ethernet, MPLS-TP, ERPS, Ethernet OAM, service types.
6. `06-otn-dwdm-cwdm.md` — G.709 OTN, wavelength grids, amplifiers, ROADMs, OSNR-limited design.
7. `07-protection-restoration-physical-diversity.md` — ring/linear protection, switch-time, SRLG — technical basis for Rule 1.
8. `08-synchronization-timing.md` — PRC/PRTC, SSU, SyncE, PTP, holdover — technical basis for Rule 5.
9. `09-capacity-dimensioning-service-mapping.md` — per-subsystem service matrix, oversubscription, growth margin — technical basis for Rule 2.
10. `10-rail-trackside-tunnel-fibre-routing.md` — tunnel/viaduct/at-grade routing, cross-passage, cable fault recovery, EMC with traction power.
11. `11-og-pipeline-plant-offshore-fibre.md` — pipeline-corridor routing, plant rings, hazardous-area optical power, subsea/offshore.
12. `12-network-management-oam.md` — NMS scope, OAM layers, alarm correlation, performance monitoring.
13. `13-power-environment-node-sites.md` — DC power, battery autonomy, node-room environment.
14. `14-cybersecurity-transport-network.md` — management-plane security, IT/OT segmentation, encryption options, vendor compliance.
15. `15-testing-commissioning-acceptance.md` — OTDR/insertion-loss, BER and service activation tests, sync verification.
16. `16-interfacing-other-subsystems.md` — ICD requirements with GSM-R, TETRA, SCADA, CCTV, PAGA, PABX, master clock.

## Status

Transmission was added 03-Oct-26 as the sixth built subsystem, from public standards knowledge (v0.1, pending gap-fill round against Harish's own project reference material).
