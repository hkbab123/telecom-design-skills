# Standards referenced by this skill

This skill references these standards by name/number and describes what each governs. It does not reproduce their copyrighted text — obtain the actual documents from their publishing bodies.

| Standard | Publisher | Governs |
|---|---|---|
| **IEC 62443 series** | IEC/ISA | Industrial automation and control systems (IACS) cybersecurity — zones and conduits, security levels, IT/OT segmentation. Governs every network-segmentation and cybersecurity item in this skill. |
| **IEC 61508** | IEC | Functional safety of electrical/electronic/programmable electronic safety-related systems — the base standard behind SIL and the SIS/SCADA independence principle. |
| **IEC 61511** | IEC | Functional safety for the process industry sector specifically (Safety Instrumented Systems) — the process-industry-specific application of IEC 61508, governing the SIS/ESD boundary referenced throughout this skill for O&G. |
| **IEC 60870-5 series** (particularly -101, -104) | IEC | Telecontrol protocols — widely used for RTU-to-SCADA communication in rail/utility and some O&G telemetry applications. |
| **IEC 61131-3** | IEC | Programmable controller programming languages — the standard PLC logic is typically written against (ladder logic, structured text, function block, etc.). |
| **DNP3** (IEEE 1815) | IEEE | An alternative telecontrol protocol to IEC 60870-5, common in North American and some utility/O&G SCADA deployments. |
| **OPC-UA (IEC 62541)** | IEC/OPC Foundation | A platform-independent, service-oriented protocol increasingly used for SCADA/historian/enterprise-layer data exchange, replacing older OPC-Classic implementations. |
| **ISA-95 (IEC 62264)** | ISA/IEC | Enterprise-control system integration — the layer model (field/control/supervisory/MES/ERP) this skill's architecture fundamentals file is built on. |
| **EEMUA 191** | EEMUA | Alarm systems — a design and management guide (not a formal international standard, but the de facto industry reference) for alarm rationalisation, priority, and target alarm rates. |
| **NFPA 130** (or the applicable national/local equivalent) | NFPA (US) / national code bodies elsewhere | Fixed guideway transit and passenger rail systems — governs tunnel-ventilation emergency/fire-mode design requirements in many jurisdictions; always confirm which code (NFPA 130, a national equivalent, or a project-specific fire engineering brief) actually governs a given rail project, never assume NFPA 130 applies outside jurisdictions that adopt it. |
| **IEC 60079 series** | IEC | Explosive-atmosphere (hazardous-area) equipment and installation requirements — governs every O&G Stage 2/3 hazardous-area item in this skill, the same as in the TETRA and PAGA subsystems. |
| **ATEX Directives (2014/34/EU) / IECEx Scheme** | European Commission / IEC | The certification regimes demonstrating IEC 60079 compliance — confirm which regime (or both) applies for a given project's jurisdiction. |

## What's out of scope for this public skill

Licensed or proprietary OEM documentation (Siemens, Schneider Electric, Honeywell, ABB, Rockwell, GE, or any other vendor's internal technical manuals) is never included in this skill. Where a decision needs an OEM-specific figure, the skill will say "confirm with OEM" rather than invent one — see the Design Rules in `SKILL.md`. Detailed SIS/ESD internal design (the safety-system's own logic and certification) is also out of scope here — this skill covers the SCADA side of the SIS/SCADA boundary only; SIS design itself is a separate functional-safety engineering discipline.

## Content basis and its limits

This skill's stage sequences were built from public SCADA/industrial-control standards knowledge and general control-systems design practice, not from a specific real project (unlike this repo's GSM-R skill, which draws on a worked project reference). Harish has direct project experience in this domain and plans to supply project-specific reference material as a later gap-fill round, the same pattern used to refine the TETRA skill's Typical-Info coverage. Treat protocol choices, I/O counts, and reliability-target figures in this skill as illustrative starting points to confirm against the actual governing standard, national regulator, and client requirement for each project.

## Next steps for this subsystem family

CCTV and fibre backbone/transmission are next planned subsystems in this family — see the repo README's roadmap.
