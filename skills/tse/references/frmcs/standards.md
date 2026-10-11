# Standards Basis — FRMCS

FRMCS standardisation is still evolving. Treat every row as a pointer to a document family whose current release and status must be checked at the source (Rule 4).

| Standard / document family | Publisher | Governs |
|---|---|---|
| FRMCS User Requirements Specification (URS), Functional Requirements Specification (FRS), System Requirements Specification (SRS) | UIC | Railway user, functional and system requirements for FRMCS |
| 3GPP TS 22.289 | 3GPP | Stage-1 requirements for a mobile communication system for railways |
| 3GPP TS 22.280, TS 22.179, TS 22.282, TS 22.281 | 3GPP | Mission-critical services: common requirements, MCPTT, MCData, MCVideo |
| 3GPP TS 23.280, TS 23.379, TS 23.282, TS 23.281 | 3GPP | Mission-critical services: common functional architecture, MCPTT, MCData, MCVideo (stage 2) |
| 3GPP TS 23.501 / TS 23.502 / TS 23.503 | 3GPP | 5G system architecture, procedures and policy/QoS framework (including 5QI table) |
| 3GPP TS 33.180, TS 33.501 | 3GPP | Security of mission-critical services; 5G system security |
| 3GPP TS 38 series, TS 36 series | 3GPP | 5G NR and LTE radio specifications |
| ETSI technical committee on railway telecommunications (FRMCS reports and specifications) | ETSI | FRMCS system concept, architecture and test specifications; verify current document numbers |
| ECC/CEPT decisions and EU implementing decisions on railway bands | CEPT / European Commission | Harmonised spectrum use for railway mobile communication; verify current text and national implementation |
| ERA / EU TSI CCS (as revised) | ERA / EU | Control-command and signalling interoperability requirements and the GSM-R-to-FRMCS transition; verify current text |
| ETCS/ERTMS data-communication specifications (including Euroradio) | UNISIG / ERA | Train-control data transport requirements the bearer must satisfy; verify the IP-bearer baseline |
| EN 50126 / EN 50128 / EN 50129 | CENELEC | Railway RAMS, software and safety-related electronic systems |
| EN 50159 | CENELEC | Safety-related communication in transmission systems |
| CLC/TS 50701 | CENELEC | Railway cybersecurity |
| IEC 62443 series | IEC | Industrial network and system cybersecurity (zones and conduits) |
| EN 50121 series, EN 50155, EN 50125 | CENELEC | Railway EMC; on-board electronic equipment; environmental conditions |
| ITU-T G.8271, G.8275.1, G.8272 | ITU-T | Time/phase synchronisation for TDD radio backhaul |

## What's out of scope

- Proprietary OEM FRMCS, 5G RAN and core internal documentation, feature licences and pricing.
- Public mobile network operator design beyond what a railway customer sees (service levels, slicing, roaming interfaces).
- Satellite and non-3GPP bearers beyond noting them as options in `fundamentals/11-onboard-gateway-multi-bearer.md`.
- Signalling system design itself (ETCS, ATO logic); only the communication requirements are covered.
- GSM-R design; see the separate GSM-R subsystem. This folder defines only the coexistence and migration boundary.

## Content basis limits

Built entirely from public UIC/3GPP/ETSI/CEPT/CENELEC standards knowledge and general mission-critical network design practice, not a specific past project. Specification numbers, release content and band allocations were written from general knowledge and must be re-verified against the source before use in a deliverable. All numeric figures in this subsystem are illustrative; verify against the governing specification, regulator, vendor documentation and project requirements. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA, CCTV and Transmission.
