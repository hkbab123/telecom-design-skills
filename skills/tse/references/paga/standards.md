# Standards referenced by this skill

This skill references standards by name/number and describes what each governs. It does not reproduce copyrighted text — obtain actual documents from the publishing bodies.

| Standard | Body | What it governs |
|---|---|---|
| **IEC 60849** ("Sound systems for emergency purposes") | IEC | The core international standard for voice-alarm/emergency sound systems — intelligibility (STI/CIS) targets, SPL requirements, and system performance under emergency conditions. Governs the acoustic-design decisions (Stage 2 item 3, Stage 3 item 5) throughout this skill. |
| **EN 54-16 / EN 54-24** (Voice Alarm Control and Indicating Equipment / Loudspeakers) | CEN | The European fire-alarm-system standard series' voice-alarm parts — equipment performance, loudspeaker performance under fire-alarm conditions, and (critically) line/loop supervision requirements. Governs Stage 2 item 9 (supervision/fault monitoring) and much of the equipment-selection basis. |
| **ISO 7240 series** (Fire detection and alarm systems) | ISO | The broader international fire-detection-and-alarm-system standard family; the voice-alarm-specific parts parallel EN 54-16/24's scope internationally. Confirm which regional standard (EN 54 vs a national/ISO-aligned equivalent) actually governs the project's jurisdiction. |
| **ISO 8201-1** (Audible emergency evacuation signal) | ISO | Defines the internationally recognised evacuation alarm tone — referenced in Stage 2 item 7 (message and tone design) where an internationally recognisable evacuation signal is required rather than a purely local/site-specific tone. |
| **IEC 60079 series** | IEC | Explosive-atmosphere (hazardous-area) equipment and installation requirements — hazardous-area zoning (IEC 60079-10), equipment certification categories (IEC 60079-0 and part-specific standards per protection type), installation practice (IEC 60079-14). Governs every O&G hazardous-area item in this skill (loudspeakers, horns, junction boxes, cable glands). |
| **ATEX Directives (2014/34/EU) / IECEx Scheme** | European Commission / IEC | The certification regimes equipment manufacturers use to demonstrate IEC 60079 compliance — ATEX for equipment placed on the EU market, IECEx as the broader international scheme many other jurisdictions reference or require. Confirm which regime (or both) applies to the project's jurisdiction. |
| **IEC 61508 / IEC 61511** | IEC | Functional safety standards — referenced wherever the General Alarm function is determined (Stage 2 item 6) to require a formal Safety Integrity Level (SIL) rating, most commonly on O&G process facilities where GA is part of the site's overall safety case. Governs the dedicated functional-safety design and verification package in Stage 3 item 11. |
| **National/local fire code** | Country- and often city-specific | Fire-survival cable rating requirements, battery-autonomy targets, evacuation-tone requirements, and overall system approval/sign-off authority. Always country- and often jurisdiction-specific — never assume one project's fire-code figures carry over to another. |
| **Marine classification society rules** (offshore only) | DNV, ABS, Lloyd's Register, etc. | Additional approval requirements for PAGA equipment installed on offshore platforms/vessels, alongside (not instead of) IEC 60079/ATEX/IECEx hazardous-area requirements. Confirm applicability and the specific classification society for offshore O&G projects. |

## What's out of scope for the public skill

Licensed/proprietary OEM documentation (Honeywell, GAI-Tronics, Stentofon/Zenitel, Hoyles, or any other vendor's internal technical manuals) is never included in this skill. Where a decision needs an OEM-specific figure, the skill says "confirm with OEM." SPL/STI targets, battery-autonomy figures, and SIL-level examples throughout this skill are illustrative starting points to confirm against the actual governing standard, national fire code, and client HSE case for the project — not settled defaults.

## Next subsystems

SCADA, CCTV, and fibre backbone are the next planned subsystems in the family — see the repo README's roadmap.
