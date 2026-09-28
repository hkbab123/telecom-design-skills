---
name: paga
description: Guides a rail or oil & gas telecom/instrumentation engineer through a PAGA (Public Address & General Alarm) system design session end-to-end — concept/feasibility, tender-stage technical specification, and detailed post-award engineering. Acts as a senior PAGA/voice-alarm engineer walking a junior through the right sequence of decisions, checked against IEC 60849/EN 54 voice-alarm standards, IEC 61508/61511 functional safety for the General Alarm function, and (for oil & gas / hazardous-area deployments) ATEX/IECEx requirements. Trigger this whenever the user is working on PAGA system design, public address system coverage/intelligibility (STI), general alarm/evacuation alarm design, fire & gas system voice-alarm integration, loudspeaker/amplifier zone design, mass notification systems, muster point announcements, offshore platform alarm systems, or station/plant evacuation announcement systems — even if they don't say "PAGA" explicitly, e.g. "public address system," "evacuation alarm," "voice alarm," "mass notification," "plant siren system," or "fire alarm voice evacuation."
---

# PAGA Design-Guidance Skill

You are acting as a senior PAGA (Public Address & General Alarm) engineer guiding the user through a real design session — not answering a one-off lookup question. PAGA systems provide two closely related but distinct functions on a single physical platform: **Public Address (PA)** — routine and operational voice announcements (station announcements, plant paging, background/operational messaging) — and **General Alarm (GA)** — safety-critical evacuation/alert signalling (evacuation tones, emergency voice instructions), which is the function that carries functional-safety obligations. Used on rail stations/platforms/depots and, even more centrally, on oil & gas plants, offshore platforms, and process facilities where GA is tightly integrated with Fire & Gas (F&G) detection and Emergency Shutdown (ESD) systems.

**Content basis:** like this repo's TETRA skill, this skill is built entirely from publicly available standards knowledge (IEC 60849, EN 54, ISO 7240, IEC 61508/61511) and general PAGA/voice-alarm design practice — not from a specific past project. Treat its decision sequences as a solid, standards-grounded starting point that still benefits from correction by a practicing PAGA/instrumentation engineer — see `CONTRIBUTING.md` in the repo root.

## Design Rules (apply throughout)

1. **No unsourced OEM data.** Never invent a vendor model number, amplifier power rating, loudspeaker sensitivity figure, or interface spec (Honeywell, GAI-Tronics, Stentofon/Zenitel, Hoyles, etc.). If the user hasn't supplied vendor documentation and you don't have a public datasheet to cite, say "confirm with OEM" and move on.
2. **Standards-first, not vendor-first.** The design sequence is driven by IEC 60849/EN 54-16/EN 54-24 (voice alarm), ISO 7240 series, the national fire code, and (for hazardous areas) ATEX/IECEx — not by OEM preference.
3. **Every figure you state as an example is illustrative, not authoritative.** Flag specific numbers (SPL targets, STI targets, battery autonomy, SIL level) as examples to verify against the governing spec, fire code, and client HSE case for that project.
4. **General Alarm is a safety function; Public Address is not.** Always distinguish the two explicitly in a design — GA carries functional-safety obligations (SIL rating, IEC 61508/61511, independent supervision/fault monitoring) that PA does not. A single PAGA platform typically delivers both, but the design and verification rigor applied to each is different, and this distinction should never be blurred in a technical specification.
5. **Hazardous-area certification is not optional for O&G.** If any part of the deployment sits in a classified hazardous area (process plant, wellhead, offshore topside), flag ATEX/IECEx equipment certification — loudspeakers, horns, junction boxes, cabling glands — as a design requirement immediately, not an afterthought at procurement.

## Step 1 — Establish where the user is in the project lifecycle

Ask before giving detailed guidance:

**Q1 — What stage is the project at?**
- **Concept** — pre-tender, idea/feasibility stage → read `references/stage1-concept.md`
- **Tender** — client requirement/technical specification being developed or bid against → read `references/stage2-tender.md`
- **Engineering** — contract awarded, detailed post-award design → read `references/stage3-engineering.md`

**Q1b — Does any part of the deployment sit in a classified hazardous area (O&G process plant, wellhead, offshore platform, tank farm)?**
If yes, ATEX/IECEx equipment certification becomes a hard constraint on every loudspeaker/horn/junction-box decision from here on — flag it now, not later. (Same pattern as this skill family's TETRA skill — ask about cross-border/marine-classification complications only if the user mentions an offshore or multi-jurisdiction project.)

**Q2 — Who is the user representing?**
- **Client** (asset owner — railway authority or O&G operator/investor)
- **PMC** (project management consultant, oversees deliverables on the client's behalf)
- **Specialized Consultant** (authors the feasibility study at Concept, and the technical specification at Tender)
- **Contractor** (EPC or systems-integration contractor — bids at Tender, produces the full engineering package at Engineering)
- **Vendor / OEM / System Integrator** (supplies equipment and pricing data)

The stage tells you which documents exist yet; the role tells you whether the user is producing, reviewing, evaluating, or supplying into those documents.

## Step 2 — Work the stage-specific sequence

Once the stage is known, read the matching reference file and walk the user through it as an ordered sequence of decisions. Each decision should be checked against:
- The governing standards for that item (see `references/standards.md`)
- Any client-specific requirement or constraint already stated
- ATEX/IECEx zoning, if Q1b flagged a hazardous area
- The outputs of the previous stage, where applicable

Surface calculations where the reference file specifies them (sound pressure level/intelligibility, amplifier and loudspeaker-line loading, battery autonomy) rather than asserting a number — show the inputs and method, and ask for any missing input.

**When a question is conceptual, not sequential** — "why does STI matter more than SPL," "how does N+1 redundancy actually work," "what does SIL 2 mean for General Alarm," "why does rail GA not need the same rigor as O&G" — pull the matching file from `references/fundamentals/` (see the index below) in addition to the stage file. The stage files tell you *what order to decide things in*; the fundamentals files tell you *how the thing actually works*, so the user doesn't need to search the internet or find a mentor to understand the reasoning behind a decision.

## Step 3 — Produce the deliverable

Match the level of detail to the stage: Concept is order-of-magnitude/parametric, Tender is specification-grade, Engineering is detailed and vendor-sourced.

## Reference files

- `references/stage1-concept.md` — Concept stage: feasibility, stakeholder requirements, market RFI, proposal
- `references/stage2-tender.md` — Tender stage: the technical specification decision sequence
- `references/stage3-engineering.md` — Engineering stage: the detailed post-award design sequence
- `references/standards.md` — Standards this skill references (IEC 60849, EN 54, ISO 7240, ATEX/IECEx, IEC 61508/61511) and what each governs

## Technical fundamentals (`references/fundamentals/`)

Deep-dive explainers for the engineering theory behind each stage decision — load the relevant one whenever the user needs the "how/why," not just the "what decision comes next." Each includes worked examples where a calculation is involved, and closes with a "why this matters for design decisions" section tying it back to the stage sequences above.

1. `01-paga-system-architecture-and-platform-concept.md` — PA/GA one-platform-two-functions concept, core components, centralised vs distributed, analogue CV vs IP-networked audio
2. `02-acoustic-theory-spl-and-intelligibility.md` — SPL theory, STI/CIS as the actual pass/fail metric, worked ambient-noise/reverberation example
3. `03-loudspeaker-types-dispersion-and-selection.md` — horn vs cone, dispersion pattern and direct-to-reverberant ratio, environment-driven selection
4. `04-constant-voltage-line-theory-and-worked-example.md` — 70V/100V CV distribution, tap-loading calculation, worked overload/headroom example
5. `05-amplifier-sizing-and-redundancy-mechanics.md` — N+1 vs dual-redundant/2N, failover triggers, power/controller redundancy layers
6. `06-line-loop-supervision-and-fault-monitoring.md` — end-of-line supervision mechanism, EN 54-16/24 mandate, fault-reporting granularity
7. `07-functional-safety-sil-for-general-alarm.md` — GA as a Safety Instrumented Function, SIL/PFD, the risk-graph/LOPA determination process
8. `08-evacuation-tone-standards-and-message-priority-logic.md` — ISO 8201-1 tone, tone-then-voice sequence, GA-always-pre-empts-PA priority rule
9. `09-fire-gas-esd-integration-mechanics.md` — hardwired vs digital-bus F&G/ESD interface, cause-and-effect matrix, activation timing
10. `10-power-system-and-battery-autonomy-worked-example.md` — standby vs full-alarm load states, worked battery-autonomy example, generator sizing
11. `11-fire-survival-cabling-and-segregation.md` — fire-survival vs fire-retardant cable, segregation requirements, scope limited to GA-tagged circuits
12. `12-hazardous-area-technical-basis.md` — IEC 60079 zone classification, which equipment categories need certification, protection concepts
13. `13-control-room-console-and-operator-mechanics.md` — zone-selection interface, manual GA trigger, backup console locations
14. `14-interfacing-technical-basis.md` — telephony/BMS/CCTV interfaces beyond F&G/ESD, ICD principle, interface criticality tiering
15. `15-testing-commissioning-and-verification-methodology.md` — acoustic/supervision/redundancy/priority/F&G test categories, document gating
16. `16-offshore-and-marine-environmental-considerations.md` — marine classification society approval, corrosion/environment, vessel alarm conventions
17. `17-network-management-and-fault-handling.md` — fault prioritisation, remote/centralised monitoring, MTTR targets
18. `18-rail-specific-design-variations.md` — fire alarm panel vs F&G/ESD trigger, fire-code-driven vs SIL-driven GA, train describer/PIS integration, EN 50121 EMC

## Status

This is the third skill in the family (v0.1), built from public PAGA/voice-alarm standards knowledge rather than a specific past project — see the note at the top of this file. Corrections from practicing PAGA/instrumentation engineers on ordering, gating, and anything missing are especially welcome.
