# Stage 2 — Tender (client requirement development)

This is where this skill's core value sits: helping the engineer build the TETRA technical requirement specification by combining the applicable standards/inputs carried over from Concept with TETRA technology know-how.

## Actors and sequence

1. PMC + specialized TETRA Consultant engaged by client.
2. Consultant takes **Stage 1 outputs as input**: applicable standards, stakeholder requirements (including HSE for O&G), high-level proposal/technology direction.
3. Consultant **builds the TETRA technical specification**, working through the decision sequence below.
4. Completed specification becomes part of the **tender package** contractors/system integrators bid against.
5. In parallel, the Consultant goes back to the market for **more accurate pricing**.
6. This results in an **Approved Vendor List (AVL)** and typically OEM/integrator shortlisting.

## Technical specification decision sequence

Work through these in order.

1. **Coverage philosophy** — continuous vs zone-specific coverage; coverage target (field-strength/signal-quality threshold for reliable voice, percentage area/location probability); special-area coverage rules — for rail: platforms, yards, depots, tunnels; for O&G: process areas, tank farms, control rooms, offshore decks, and — critically — **in-building coverage inside plant structures**, which is often the hardest and most safety-relevant part of an O&G TETRA design.
2. **Hazardous-area zoning and equipment certification (O&G — do this early, not late)** — obtain or commission the site's hazardous-area classification drawing (Zone 0/1/2 per IEC 60079, or Division 1/2 in North American practice); every handset, base station, antenna, and cabling item sited or used inside a classified zone must carry the matching ATEX and/or IECEx certification (Ex ia, Ex d, etc. per zone). This constrains equipment choice for the rest of the sequence — flag it as a hard gate on item 9 (equipment dimensioning), not a late-stage checklist item.
3. **SwMI architecture / network topology** — Switching and Management Infrastructure (SwMI) sizing and siting: number and siting logic of exchanges/switches (DXT or equivalent), number of base station sites, dispatcher/control-room architecture, redundancy of the SwMI core (see item 4). Decide single-site vs multi-site trunked network vs a simulcast/wide-area design.
4. **Redundancy and availability targets** — network-level availability target (higher for O&G process-safety-linked comms than for a purely administrative rail depot network — state the target explicitly per use case rather than assuming one figure fits both); SwMI core redundancy (dual/hot-standby exchange); base-station site redundancy (backup power autonomy, especially for remote O&G field sites without grid power); ring/star transmission protection between sites.
5. **Frequency planning** — the specific PMR band allocated by the national regulator for this project (varies by country — commonly somewhere in the 380–470 MHz range for TETRA, but never assume without checking the regulator's actual allocation for this project); channel/frequency reuse plan across sites; interference coordination with adjacent licensed users in the same band.
6. **Fleet mapping and talkgroup design** — organise users into talkgroups by operational function (e.g. for rail: station ops, yard/shunting, maintenance, security; for O&G: control room, field operations, maintenance, HSE/emergency response, contractors); design the talkgroup hierarchy, scan lists, and any dynamic group number assignment (DGNA) requirement; decide emergency-call handling and priority call/pre-emption policy.
7. **Trunking / capacity dimensioning (Erlang)** — Erlang-B (or Erlang-C if queuing is acceptable for non-priority traffic) traffic modelling per site, based on expected call attempts per busy hour per talkgroup; number of traffic channels per base station; separate voice from any data-channel (TETRA SDS/packet data) provision if data terminals or telemetry are in scope.
8. **Link budget / coverage calculation** — path loss modelling appropriate to the environment (open yard vs dense plant structure with significant clutter/absorption vs tunnel — each needs a different propagation model); fade margin; equipment cable/combiner losses; in-building penetration loss allowance for O&G plant structures; uplink/downlink balance (handheld TX power is usually the limiting link).
9. **Equipment dimensioning and selection basis** — base station/repeater sizing per site, SwMI exchange capacity, dispatcher console count, handheld/mobile radio count and type (including which units must be ATEX/IECEx-certified per item 2), DMO repeater/gateway count if Direct Mode is in scope (see item 10), vehicle-mounted radio count, site cabinet and power system sizing.
10. **Direct Mode Operation (DMO) requirement** — decide whether off-network direct radio-to-radio communication is required (common for O&G field/emergency-response teams working outside trunked coverage, or as a fallback if the trunked network fails); if yes, specify DMO gateway/repeater coverage and how DMO traffic interoperates with the trunked (TMO) network.
11. **Encryption and security** — air-interface encryption grade (TEA1/TEA2/TEA3/TEA4 — the applicable algorithm is regulator- and jurisdiction-dependent, confirm rather than assume); whether end-to-end encryption is required on top of air-interface encryption (common for security/emergency-response talkgroups); authentication method between terminals and the SwMI; policy on over-the-air rekeying.
12. **Functional & operational feature design** — dispatcher console functional requirements (talkgroup patch/cross-connect, priority override, ambience listening per organisational policy and local law, individual call, status/short data messaging); emergency call/emergency button behaviour and routing; lone-worker/man-down feature requirement if applicable; fleet management/GPS location reporting if in scope.
13. **Interfaces** — list explicitly, by family: **telephony** (TETRA ↔ PABX/PSTN gateway for interconnect calls); **O&M and asset systems** (TETRA ↔ SCADA/central alarm for O&G, TETRA ↔ maintenance-management/fault-logging, TETRA ↔ voice recording system); **adjacent radio networks** (TETRA ↔ any legacy analogue PMR being phased out, or GSM-R/rail systems if this project sits alongside one); **dispatcher/control-room systems** (integration with the operational control centre or plant control room).
14. **Regulatory approvals** — frequency/spectrum licence application to the national telecom regulator; equipment type-approval requirements; ATEX/IECEx certification verification for all hazardous-area equipment (item 2); interference coordination with adjacent licensed PMR users.
15. **Availability/reliability KPIs and safety case basis** — numeric targets bidders must commit to (network availability %, MTBF/MTTR for base stations and SwMI core, call setup time, coverage percentage). For O&G deployments where TETRA carries emergency-response or process-safety-linked traffic, treat this as a safety-relevant system and reference the client's applicable functional-safety framework (e.g. IEC 61508/61511-derived requirements, or the client's own HSE case methodology) rather than assuming a generic PMR reliability target is sufficient.
16. **Compliance matrix** — map every requirement above to the relevant ETSI TETRA standard clauses, the national regulator's licence conditions, and (for O&G) the applicable hazardous-area and functional-safety standards.
17. **Tender-grade BOQ and testing/acceptance criteria** — high-level bill of quantities basis; FAT/SAT acceptance criteria bidders must commit to, including a hazardous-area equipment certification verification step for O&G.
18. **Verification & QoS strategy** — pre-commissioning field measurement campaign (coverage survey against the target from item 1) with independent verification; for O&G, coordinate the field survey with the site's HSE/permit-to-work requirements for entering classified zones.

## Inputs

Stage 1 outputs; PMC's oversight requirements/format standards; hazardous-area classification data (O&G).

## Deliverables

TETRA technical specification (for tender), refined/accurate pricing data, Approved Vendor List, OEM selection outcome, compliance matrix against standards.

## Roles

- **Consultant** — builds the technical specification, runs the refined market pricing exercise
- **PMC** — oversees the Consultant's deliverables on the client's behalf
- **Client** — engages PMC + Consultant, ultimately owns the resulting tender
- **Contractor** — bids against the tender package
- **Vendor/OEM/SI** — provides accurate pricing, ends up on the Approved Vendor List

All figures in this file (frequency bands, encryption algorithm names, reliability targets) are illustrative and jurisdiction/regulator-dependent — confirm the actual applicable figure or standard clause against the governing spec and national regulator for each project, never assume they carry over unchanged from another country or a rail context into an O&G one or vice versa.
