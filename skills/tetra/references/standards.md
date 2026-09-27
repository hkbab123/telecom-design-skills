# Standards referenced by this skill

This skill references these standards by name/number and describes what each governs. It does not reproduce their copyrighted text — obtain the actual documents from their publishing bodies.

| Standard | Publisher | Governs |
|---|---|---|
| **ETSI EN 300 392 series** ("TETRA Voice+Data") | ETSI | The core TETRA air-interface, network, and services standard — trunking, group call, DMO, SDS/data, and the encryption framework the algorithm choices (TEA1–TEA4) sit inside. |
| **ETSI TS 100 392 series** | ETSI | Detailed technical specifications underlying the EN 300 392 series (protocol testing, interworking, etc.). |
| **IEC 60079 series** | IEC | Explosive-atmosphere (hazardous-area) equipment and installation requirements — the reference for hazardous-area zoning (IEC 60079-10), equipment certification categories (IEC 60079-0 and part-specific standards for each protection type), and installation practice (IEC 60079-14). Governs every O&G Stage 2/3 hazardous-area item in this skill. |
| **ATEX Directives (2014/34/EU) / IECEx Scheme** | European Commission / IEC | The certification regimes that equipment manufacturers use to demonstrate IEC 60079 compliance — ATEX for equipment placed on the EU market, IECEx as the broader international scheme many other jurisdictions reference or require. Confirm which regime (or both) applies for a given project's jurisdiction. |
| **National telecom regulator requirements** | Country-specific | PMR frequency band allocation, spectrum licensing, and equipment type-approval — always country-specific; never assume a band or licensing process carries over from one country to another. |
| **IEC 61508 / IEC 61511** | IEC | Functional safety standards relevant where TETRA carries emergency-response or process-safety-linked traffic on an O&G site — referenced as the Stage 2 item 15 safety-case framework where the client's own HSE case methodology doesn't already cover it. |
| **EN 50126** (where a rail deployment sits alongside a GSM-R or other safety-critical rail system) | CENELEC | RAMS methodology — relevant if the TETRA network's reliability needs to be argued in the same framework as an adjacent safety-critical rail system, even though TETRA itself is typically non-safety-critical on rail (station/yard/depot voice, not train control). |

## What's out of scope for this public skill

Licensed or proprietary OEM documentation (Motorola, Hytera, Airbus, Sepura, or any other vendor's internal technical manuals) is never included in this skill. Where a decision needs an OEM-specific figure, the skill will say "confirm with OEM" rather than invent one — see the Design Rules in `SKILL.md`.

## Content basis and its limits

This skill's stage sequences were built from public TETRA standards knowledge and general PMR design practice, not from a specific real project (unlike this repo's GSM-R skill, which draws on a worked project reference). Treat frequency-band examples, encryption-algorithm choices, and reliability-target figures as illustrative starting points to confirm against the actual governing standard, national regulator, and client requirement for each project — not as settled defaults.

## Next steps for this subsystem

PAGA, SCADA, CCTV, and fibre backbone are the next planned subsystems in this family — see the repo README's roadmap.
