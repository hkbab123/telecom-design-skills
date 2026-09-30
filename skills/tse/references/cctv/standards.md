# Standards Basis — CCTV / Video Surveillance System

| Standard | Publisher | Governs |
|---|---|---|
| IEC 62676 series | IEC | Video surveillance systems for security applications — system requirements, performance, IP interoperability (62676-2), image quality |
| ONVIF Profile S/T/G/Q | ONVIF | IP camera/VMS interoperability — streaming (S), advanced streaming/analytics metadata (T), storage/recording (G), access control (Q) |
| IEC 60839 series | IEC | Alarm and electronic security systems — general requirements, overlaps with CCTV/access-control integration |
| BS EN 50132 | BSI (regional/historical) | Older European CCTV standard, largely superseded by IEC 62676 — relevant on brownfield/legacy European projects |
| ISO/IEC 27001 (referenced) | ISO/IEC | Information-security management — referenced for VMS network/cybersecurity governance, alongside SCADA's IEC 62443 discipline |
| IEC 60079 series / ATEX (2014/34/EU) / IECEx Scheme | IEC / EU / IECEx | Hazardous-area equipment/installation for O&G camera housings and cabling |
| National data-protection regime (e.g. GDPR or local equivalent) | National/regional regulator | Footage retention, access, and privacy — always confirm the applicable regime for the specific jurisdiction |

## What's out of scope

- Proprietary OEM VMS/analytics internal documentation.
- Detailed law-enforcement evidentiary chain-of-custody procedure design — this skill covers the technical system (coverage, recording, retention, access control) that supports an evidentiary requirement, not the legal/procedural chain-of-custody process itself.
- Detailed intrusion-detection or fire/gas-detection system design — this skill covers the CCTV/VCA verification layer only, per the detection-vs-verification boundary (rule 1); the detection system itself is a separate subsystem.

## Content basis and its limits

Built entirely from public IEC 62676/ONVIF/IEC 60839 standards knowledge and general VSS design practice, not from a specific past project. Harish may supply project-specific reference material later as a gap-fill round, same pattern as SCADA.

## Next steps for this subsystem family

Fibre backbone/transmission (SDH/NG-SDH/FG-OTN/DWDM) is next on the roadmap, alongside the "new strong candidates" pool (PABX, VSAT, Master Clock, Security & Access Control, PIDS, Marine/Aero radio, Station Management Systems, Platform Screen Doors).
