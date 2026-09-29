# Stage 2 — Tender (client requirement development)

This is where this skill's core value sits: helping the engineer build the GSM-R technical requirement specification by combining the applicable standards/inputs carried over from Concept with GSM-R technology know-how. GSM-R is one subsystem specification among several produced in parallel at this stage (TETRA, PAGA, SCADA, etc. are siblings built the same way).

## Actors and sequence

The client engages a **PMC** (oversight role) plus a **specialized GSM-R Consultant** (may or may not be the same firm as the Stage 1 Consultant) to develop the technical requirement.

1. PMC + specialized GSM-R Consultant engaged by client.
2. Consultant takes **Stage 1 outputs as input**: applicable standards, stakeholder requirements, high-level proposal/technology direction.
3. Consultant **builds the GSM-R technical specification**, working through the 18-point decision sequence below.
4. Completed specification becomes part of the **tender package** EPC contractors bid against.
5. In parallel, the Consultant goes back to the market for **more accurate pricing** from OEMs/system integrators (more refined than the Stage 1 budgetary RFI).
6. This results in an **Approved Vendor List (AVL)** and typically OEM selection/shortlisting.

## The 18-point technical specification decision sequence

Work through these in order — each depends on decisions made earlier in the list. Where a project is cross-border, the core-placement decision (item 2) drives choices in several later items — flag that dependency as you go.

1. **Coverage philosophy** — continuous track coverage vs discontinuous; coverage class/target (EIRENE-aligned field strength thresholds for cab-level reception, percentage location probability); special-area coverage rules for tunnels, stations, yards, depots, marshalling areas.
2. **Redundancy and availability targets** — network-level availability target (often 99.9%+ for safety-relevant voice, EIRENE-driven); redundancy philosophy for BSC/MSC (N+1), transmission ring protection, dual-homing of base stations, backup power autonomy at sites. **If cross-border**, decide core placement here: an independent core per country with interworking (recommended default) vs a single shared network with geographically split control centres (weaker, but used on some past projects — present both, don't default silently).
3. **Frequency planning** — R-GSM 900 (and E-GSM extension where applicable) band plan; frequency reuse pattern; guard-band/interference coordination with adjacent public GSM operators; cross-border frequency coordination if the line crosses a border.
4. **Network architecture / topology** — BSS/NSS architecture, number and siting logic of BSC/MSC nodes, dispatcher/OCC architecture, functional numbering/addressing plan, group call (VGCS) and voice broadcast (VBS) architecture, eMLPP priority scheme. If cross-border, this is where the core-placement decision from item 2 gets architected out (per-country cores + interworking gateway, vs shared core with primary/backup split); note which regulator/standards body governs which part of the network.
5. **Model / technology decisions** — GSM-R baseline vs any FRMCS-readiness provisions the client wants built in; equipment technology generation.
6. **Cell planning** — cell radius and site spacing driven by line speed (Doppler shift compensation); handover design (EIRENE handover time target, typically <300 ms, and overlap-zone length calculation); antenna type/orientation (directional along track vs sectorised at stations/yards); dual-overlapping-BTS-per-site as an optional redundancy pattern to evaluate.
7. **Channel / traffic planning and capacity dimensioning** — Erlang-based traffic modelling, kept separate by traffic class (operational voice, group calls, emergency calls, shunting mode, passenger vs freight vs maintenance-vehicle vs station traffic); number of TRX per site; circuit-switched vs packet-switched (GPRS/EDGE, SGSN/GGSN/PCU sizing) data channel provision if ETCS L2 or other data services are in scope.
8. **Link budget / coverage calculation** — path loss modelling (open track vs tunnel-specific models — leaky feeder + optical repeaters vs discrete antenna, with a stated redundancy target for tunnel sections); fade margins; RF aging margin; cable/combiner losses; uplink/downlink balance.
9. **Equipment dimensioning** — BTS/BSC/MSC/gateway sizing, dispatcher workstation count, cab radio and GSM-R SIM count basis (per rolling-stock fleet size), trackside cabinet and power system sizing (battery autonomy); mast structural reserve for future/third-party equipment; antenna cable-loss and return-loss/VSWR targets.
10. **Transmission/backhaul network design** — fibre backbone bandwidth dimensioning between BTS–BSC–MSC (dedicated cores on a wider multi-service transmission network where one exists); microwave links where fibre isn't available; ring protection scheme.
11. **Functional & operational feature design** — functional numbering/addressing scheme (e.g. enhanced location-dependent addressing with fallback); role-based handheld terminal categories (general-purpose, operational/maintenance, shunting) and their basis of quantity; OTA SIM management platform; dispatcher console functional requirements (push-to-talk, hold/transfer, conference, role handling, integration with local telephony/PABX).
12. **Interfaces** — list explicitly, grouped by family (these are easy to miss and often drive late-stage rework):
    - **Signalling:** GSM-R ↔ ETCS/ERTMS Radio Block Centre — communication bearer and, where used, the safe-communication/key-management layer protecting movement authorities and speed restrictions.
    - **Transmission backbone:** GSM-R traffic routing over the wider fibre/transmission backbone where one exists.
    - **Operations/O&M and asset systems:** GSM-R ↔ OCC/dispatcher; ↔ central alarm/SCADA; ↔ maintenance-management/fault-logging; ↔ voice recording system; ↔ Network Management System.
    - **Legacy/adjacent telecom:** GSM-R ↔ PABX, PAGA where integration is required.
    - **Public network:** GSM-R ↔ public GSM network (interconnection/gateway for non-safety calls, roaming agreements at borders).
    - **Power:** GSM-R ↔ power supply/monitoring systems.
    - **Cross-border:** GSM-R ↔ neighbouring rail administration's GSM-R network (per EIRENE) — architecture depends on the core-placement decision in item 2.
    - **Rolling stock:** GSM-R ↔ on-board train control/monitoring and maintenance-management systems, where wireless data reporting is in scope.
13. **Regulatory approvals** — spectrum licence application to the national telecom regulator(s) (more than one if cross-border); EIRENE compliance/interoperability certification route; equipment type-approval requirements; interference coordination agreements with public mobile operators; civil/environmental approvals for tower siting; regional interoperability mandate compliance where applicable (e.g. GCC Rail Guidelines).
14. **RAMS requirements** — reliability/availability/maintainability/safety targets per EN 50126, stated as numeric KPIs bidders must commit to (network availability %, equipment MTBF, MTTR — with a separate tighter MTTR for operations-critical failures, speech quality/MOS on radio and end-to-end, handover success rate); safety integrity level assessment for GSM-R as a safety-relevant system.
15. **Cybersecurity** — applicable cybersecurity standard (e.g. ISO/IEC 62443, or a rail-specific cybersecurity standard); encryption/authentication on radio and transport layers; protection against electromagnetic jamming; network segmentation isolating safety-critical traffic.
16. **Compliance matrix** — map every requirement above back to EIRENE FRS/SRS, relevant 3GPP/UIC clauses, and any national rail authority standard(s) (plural if cross-border), so bidders can demonstrate compliance clause-by-clause.
17. **Tender-grade BOQ and testing/acceptance criteria** — high-level bill of quantities basis, and the FAT/SAT acceptance criteria bidders must commit to.
18. **Verification & QoS strategy** — pre-commissioning field measurement campaign against a named QoS test specification, contractor-run with independent third-party verification of results; for safety-relevant systems, an independent safety assessment/audit before final acceptance.

## Inputs

Stage 1 outputs (standards applicable, stakeholder requirements, proposal); PMC's oversight requirements/format standards.

## Deliverables

GSM-R technical specification (for tender), refined/accurate pricing data, Approved Vendor List, OEM selection outcome, compliance matrix against standards.

## Roles

- **Consultant** — builds the technical specification, runs the refined market pricing exercise
- **PMC** — oversees the Consultant's deliverables on the client's behalf
- **Client** — engages PMC + Consultant, ultimately owns the resulting tender
- **Contractor** — bids against the tender package; not the producer of the spec
- **Vendor/OEM/SI** — provides accurate pricing, ends up on the Approved Vendor List

## Cross-border considerations (worked reference: real cross-border GSM-R extension)

- Core placement: **independent core per country with interworking** is the recommended default over a single shared network split only across primary/backup control centres — the latter is architecturally weaker even though some past projects have used it.
- Multiple national regulators/security agencies must be coordinated, not just one.
- A regional interoperability mandate (e.g. GCC Rail Guidelines) may be a standards input alongside EIRENE/3GPP/UIC.
- On brownfield/cross-border extensions, audit existing assets before specifying new ones — expand or replace before building isolated new systems.
- Traffic modelling should separate passenger, freight, maintenance-vehicle, and station traffic profiles explicitly.
- Dual overlapping BTS coverage per site (two independent BTS per location, each on a different BSC/core) is a redundancy pattern to offer, separate from the core-placement decision.
- Tunnel coverage is its own link-budget/architecture sub-case: leaky feeder + optical repeaters, with an explicit redundancy percentage target.
- Packet-switched core (SGSN/GGSN/PCU) sizing is its own dimensioning line when ETCS L2 data bearer is in scope, alongside the circuit-switched voice core.
- Site infrastructure specifics worth checklisting: structural reserve on masts for future/third-party equipment, antenna cable loss and return-loss/VSWR targets, and an explicit RF aging margin in the link budget — treat any specific figure as an example to verify against the current governing spec, not a fixed rule.

All figures in this file (e.g. 99.9% availability, <300 ms handover) are illustrative benchmarks drawn from EIRENE-aligned practice — confirm the actual target against the governing spec for each project.
