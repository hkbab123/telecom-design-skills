# Standards Basis — Transmission / Fibre Backbone

| Standard | Publisher | Governs |
|---|---|---|
| ITU-T G.652 / G.655 / G.657 / G.654 | ITU-T | Single-mode fibre categories (standard, non-zero dispersion-shifted, bend-insensitive, cut-off-shifted) |
| IEC 60793 series | IEC | Optical fibre specifications and test methods |
| IEC 60794 series | IEC | Optical fibre cable specifications |
| IEC 60332 / IEC 61034 / IEC 60754 | IEC | Cable flame propagation, smoke density, halogen-acid-gas emission |
| ITU-T G.707 / G.783 / G.841 | ITU-T | SDH frame structure, equipment functional blocks, protection architectures |
| ITU-T G.709 / G.872 / G.798 | ITU-T | OTN interfaces, architecture, equipment functions |
| ITU-T G.694.1 / G.694.2 | ITU-T | DWDM and CWDM wavelength grids |
| ITU-T G.957 / G.959.1 | ITU-T | Optical interface parameters (SDH and OTN physical layer) |
| ITU-T G.8031 / G.8032 | ITU-T | Ethernet linear protection and ring protection (ERPS) |
| ITU-T G.8110.1 / G.8131 | ITU-T | MPLS-TP architecture and linear protection |
| ITU-T Y.1731 / Y.1564 | ITU-T | Ethernet OAM and service-activation testing |
| ITU-T G.811 / G.812 / G.813 | ITU-T | Primary reference clock, synchronisation supply unit, SDH equipment clock |
| ITU-T G.8261 / G.8262 / G.8265.1 / G.8275.1 | ITU-T | Packet-network synchronisation, SyncE clock, PTP telecom profiles |
| IEEE 1588 | IEEE | Precision Time Protocol |
| ITU-T G.826 / G.8201 | ITU-T | Error performance parameters for SDH and OTN paths |
| MEF 10.x / MEF 6.x | MEF | Carrier Ethernet service attributes and definitions |
| IEC 61280 / IEC 61300 | IEC | Optical communication subsystem and connector test procedures |
| IEC 60825-1 | IEC | Laser product safety |
| IEC 60079-28 | IEC | Optical radiation protection in explosive atmospheres |
| IEC 62443 series | IEC | Industrial network and system cybersecurity (management plane and IT/OT boundary) |
| EN 50121 series | CENELEC | Railway EMC (relevant to trackside node equipment) |

## What's out of scope

- Proprietary OEM transmission-equipment internal documentation, feature licences and pricing.
- Subsea cable system engineering (repeatered long-haul systems); only shallow-water/short offshore links are touched, in `fundamentals/11-og-pipeline-plant-offshore-fibre.md`.
- Access networks for end customers (PON/FTTx); this skill covers the operator's own backbone and station/plant rings.
- Fibre-optic sensing (DTS/DAS leak or intrusion detection) design — noted as a thin item in `TSE Skill.md`, may become a short reference note later.

## Content basis limits

Built entirely from public ITU-T/IEC/IEEE standards knowledge and general transport-network design practice, not a specific past project. All numeric figures in this subsystem are illustrative; verify against the governing specification, vendor documentation and project requirements. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA and CCTV.
