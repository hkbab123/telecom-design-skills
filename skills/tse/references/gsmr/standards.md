# Standards referenced by this skill

This skill references these standards by name/number and describes what each governs. It does not reproduce their copyrighted text — obtain the actual documents from their publishing bodies.

| Standard | Publisher | Governs |
|---|---|---|
| **EIRENE FRS** (Functional Requirements Specification) | UIC | The functional requirements GSM-R must meet — coverage, handover, group call/VGCS, eMLPP priority, functional addressing. The primary reference for Stage 2 items 1, 4, 6, 11. |
| **EIRENE SRS** (System Requirements Specification) | UIC | The technical/system-level requirements implementing the FRS — the detailed reference for cell planning, link budget, and interface behaviour. |
| **3GPP GSM/GSM-R specifications** | 3GPP | The underlying GSM radio and network standard GSM-R is built on (R-GSM 900/E-GSM band, GPRS/EDGE where used for data). |
| **UIC standards/leaflets** | UIC (International Union of Railways) | Railway operating and interoperability practice that GSM-R design must align with, beyond the EIRENE documents themselves. |
| **EN 50126** | CENELEC | RAMS (Reliability, Availability, Maintainability, Safety) methodology for railway applications — the reference for Stage 2 item 14 and Stage 3 step 13. |
| **ISO/IEC 62443** (or a rail-specific cybersecurity standard) | ISO/IEC | Industrial/OT cybersecurity — the reference for Stage 2 item 15 and Stage 3 step 14, where a rail-specific cybersecurity standard doesn't already apply in the project's jurisdiction. |
| **Regional interoperability mandates** (e.g. GCC Rail Guidelines) | Regional bloc bodies | Additional interoperability requirements when a project sits inside a regional rail bloc — check whether one applies alongside EIRENE/3GPP/UIC. |
| **National telecom regulator requirements** | Country-specific | Spectrum licensing, type-approval, and interference-coordination requirements — always country-specific, doubled up on cross-border projects. |

## What's out of scope for this public skill

Licensed or proprietary OEM documentation (Huawei, Nokia, or any other vendor's internal technical manuals) is never included in this skill and never should be. Where a decision needs an OEM-specific figure, the skill will say "confirm with OEM" rather than invent one — see the Design Rules in `SKILL.md`. If you have legitimate access to vendor documentation for your project, supply the relevant figures yourself and the skill will use them; it won't source them independently.

## Next subsystem in this family

FRMCS (the LTE-based successor to GSM-R) is the planned second build once this GSM-R skill is stable — see the repo README's roadmap.
