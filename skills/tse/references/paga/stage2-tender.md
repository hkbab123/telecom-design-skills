# Stage 2 — Tender (client requirement development)

This is where the skill's core value sits: helping the engineer build a PAGA technical specification by combining applicable standards, the inputs carried over from Concept, and PAGA/voice-alarm domain know-how.

## Actors and sequence

1. PMC + specialized PAGA Consultant engaged by client.
2. Consultant takes **Stage 1 outputs as input**: applicable standards, stakeholder requirements (including HSE/fire engineering for O&G), high-level proposal, and the preliminary PA/GA scope split.
3. Consultant **builds the PAGA technical specification**, working through the decision sequence below.
4. Completed specification becomes part of the **tender package** contractors/system integrators bid against.
5. In parallel, Consultant goes back to the market for **more accurate pricing**.
6. Results in an **Approved Vendor List (AVL)** — typically OEM/integrator shortlisting.

## Technical specification decision sequence

Work through in order.

1. **Zone philosophy and PA/GA scope split** — define public-address zones (paging/operational announcement areas) and general-alarm/evacuation zones (which may or may not map 1:1 onto PA zones); state explicitly, per area, whether it needs PA only, GA only, or both. Special-area rules — rail: platforms, concourse, yards, depots, tunnels; O&G: process areas, control rooms, offshore living quarters/muster areas, and confined/high-noise plant spaces.
2. **Hazardous-area zoning and equipment certification (O&G — do this early)** — obtain/commission the site's hazardous-area classification drawing (Zone 0/1/2 per IEC 60079, or Division 1/2 in North American practice); every loudspeaker, horn, junction box, and cabling item sited in a classified zone must carry matching ATEX and/or IECEx certification. Constrains equipment choice for the rest of the sequence — a hard gate on item 9, not a late checklist item.
3. **Acoustic design targets** — sound pressure level (SPL) target above measured/estimated ambient noise per zone (higher in noisy plant/compressor areas than in a quiet office or control room), and speech intelligibility target expressed as Speech Transmission Index (STI) or Common Intelligibility Scale (CIS) per IEC 60849/IEC 60268-16 — the actual metric that determines whether an evacuation announcement is understandable, not just audible. State both targets explicitly per zone type rather than assuming one figure fits every area.
4. **System architecture** — central PAGA equipment rack/amplifier system siting (single central rack vs distributed zone amplifiers), zone controller architecture, and whether the system is analogue constant-voltage line, digital/IP-networked audio, or a hybrid — this choice drives most of the downstream cabling and redundancy decisions.
5. **Redundancy and availability** — amplifier redundancy (N+1 or dual-redundant, since a failed amplifier shouldn't silence a zone during an emergency), power supply redundancy, and central controller/processor redundancy; state the target explicitly, and note that the redundancy requirement for the GA function is typically stricter than for PA-only equipment given GA's safety role.
6. **Functional safety / SIL rating for General Alarm** — determine, with the client's HSE/safety function, whether the General Alarm function requires a formal Safety Integrity Level (SIL) rating under IEC 61508/61511 (common on O&G process facilities where GA is part of the site's overall safety case; less commonly formalised on a rail station, where GA is usually fire-code-driven instead). If SIL-rated, this becomes a hard constraint on architecture (item 4), redundancy (item 5), and supervision/fault-monitoring (item 9) — flag it here, don't leave it to Stage 3.
7. **Message and tone design** — the evacuation/alert tone standard to use (e.g. ISO 8201-1 for the internationally recognised evacuation tone, or the applicable national fire-alarm tone standard); pre-recorded message library scope (evacuation instructions, muster-point directions, all-clear, in the relevant site languages); live-announcement/talk-through capability from the control room or fire panel; priority and override logic — a GA/emergency announcement must always be able to override and interrupt any PA/background-music zone it shares, never the reverse.
8. **Loudspeaker and amplifier-line dimensioning** — loudspeaker type and placement per zone (horn speakers for high-noise/outdoor plant areas, ceiling/wall speakers for indoor low-noise areas), constant-voltage line design (commonly 70V or 100V line, confirm with OEM/regional practice) with per-line loudspeaker tap loading kept within amplifier capacity, and cable voltage-drop calculation for long line runs (relevant on large plant sites and long station platforms).
9. **Line/loop supervision and fault monitoring** — GA circuits (and often PA circuits too) require continuous electrical supervision of loudspeaker lines and amplifier output so a cable fault or open circuit is detected and alarmed automatically, not discovered only when the alarm fails to sound — a standard EN 54-16/EN 54-24-driven requirement, and a hard requirement if the GA function is SIL-rated (item 6).
10. **Power system and battery autonomy** — UPS/battery backup sized to keep the GA function operating for a defined period after mains-power loss (a fire-code-driven figure, commonly longer than a typical comms-system battery-autonomy target, since evacuation must remain possible during a power-loss event that may itself be part of the emergency); size against the full connected load, not just standby/quiescent draw.
11. **Cabling** — fire-resistant/fire-survival cable (rated to maintain circuit integrity for a defined duration under fire conditions, e.g. an FP-type or equivalent fire-survival cable per the applicable national standard) for GA circuits specifically; physical segregation from power cabling and from non-fire-rated PA-only cabling where required by the fire code.
12. **Equipment dimensioning and selection basis** — amplifier rack sizing, loudspeaker count and type per zone (incl. which must be ATEX/IECEx-certified per item 2), control panel/call-station count, power supply and battery sizing — every figure sourced or flagged "confirm with OEM."
13. **Interfaces** — grouped by family: **life-safety systems** (PAGA ↔ Fire Alarm Control Panel, Fire & Gas detection system, Emergency Shutdown (ESD) system — the interface that actually triggers automatic GA activation on a confirmed fire/gas event); **telephony** (PAGA ↔ PABX for operator-initiated paging); **O&M/monitoring** (PAGA ↔ central SCADA/NMS for fault reporting); **adjacent systems** (rail: PAGA ↔ passenger information system/train describer; O&G: PAGA ↔ CCTV for operator situational awareness during an event).
14. **Regulatory approvals** — national/local fire code compliance sign-off, ATEX/IECEx certification verification for hazardous-area equipment (item 2), and (offshore) marine classification society approval where applicable.
15. **Availability/reliability KPIs and safety case basis** — numeric targets (system availability %, MTBF/MTTR, SPL/STI compliance rate across zones). Where the GA function is SIL-rated (item 6), reference the applicable IEC 61508/61511 verification requirements rather than a generic reliability target.
16. **Compliance matrix** — map every requirement to the relevant voice-alarm standard clauses (IEC 60849, EN 54-16/EN 54-24, or the applicable national equivalent), fire code, and (O&G) hazardous-area/functional-safety standards.
17. **Tender-grade BOQ and testing/acceptance criteria** — BOQ basis; FAT/SAT acceptance criteria including an SPL/STI verification test methodology and a loop-supervision fault-injection test.
18. **Verification & QoS strategy** — pre-commissioning acoustic survey (SPL and STI measurement against the item 3 target) with independent verification; for O&G, coordinate with the site's HSE/permit-to-work requirements for entering classified zones to install/test equipment.

## Inputs

Stage 1 outputs; PMC's oversight/format requirements; hazardous-area classification data (O&G); ambient noise data where already available.

## Deliverables

PAGA technical specification (for tender), refined/accurate pricing data, Approved Vendor List, OEM selection outcome, compliance matrix.

## Roles

- **Consultant** — builds the spec and runs refined pricing
- **PMC** — oversees
- **Client** — owns the resulting tender
- **Contractor** — bids against it
- **Vendor/OEM/SI** — provides pricing, ends up on the AVL

All figures in this file (SPL/STI targets, battery autonomy, SIL level, cable rating) are illustrative — flag as examples to verify against the governing standard, national fire code, and client HSE case for that specific project.
