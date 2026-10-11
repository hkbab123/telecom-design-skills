# Standards Basis — Master Clock / Time Synchronisation

| Standard | Publisher | Governs |
|---|---|---|
| IEEE 1588 (IEC 61588) | IEEE / IEC | Precision Time Protocol (PTP) |
| IEEE 802.1AS | IEEE | Generalised PTP (gPTP) for bridged and time-sensitive networks |
| IEC/IEEE 61850-9-3, IEEE C37.238 | IEC / IEEE | PTP power-utility profile (substation automation) |
| IEEE C37.118.1 | IEEE | Synchrophasor measurement, including time-quality and IRIG-B time-code extensions |
| RFC 5905 | IETF | Network Time Protocol version 4 (NTPv4) |
| RFC 4330 | IETF | Simple Network Time Protocol (SNTP) |
| RFC 8915 | IETF | Network Time Security (NTS) for NTP |
| IRIG Standard 200 | Range Commanders Council | IRIG serial time codes (IRIG-B and others) |
| ITU-T G.811 / G.8272 / G.8272.1 | ITU-T | Primary reference clock (frequency), primary reference time clock, enhanced PRTC |
| ITU-T G.8271 | ITU-T | Time and phase synchronisation aspects of packet networks |
| ITU-T G.8265.1 / G.8275.1 / G.8275.2 | ITU-T | PTP telecom profiles (frequency; phase with full on-path support; phase with partial support) |
| ITU-T G.8273.2 | ITU-T | Timing characteristics of telecom boundary clocks and slave clocks |
| IEC 62443 series | IEC | Industrial network and system cybersecurity (IT/OT boundary, zones and conduits) |
| IEC 62305 series | IEC | Lightning protection (antenna and mast installations) |
| IEC 60529 / IEC 62262 | IEC | Ingress protection (IP) and impact protection (IK) ratings for outdoor and public-area clocks |
| IEC 60079 series | IEC | Explosive atmospheres (hazardous-area equipment and installation) |
| EN 50121 series | CENELEC | Railway EMC (trackside and station equipment) |
| EN 50155 / EN 50125 | CENELEC | Rail electronic equipment and environmental conditions (relevant to train-borne and trackside units) |

## What's out of scope

- Proprietary OEM master-clock and GNSS-receiver internal documentation, feature licences and pricing.
- National time-laboratory engineering (UTC(k) realisation, caesium fountain or optical-clock operation).
- Frequency and phase synchronisation inside the transport network (SyncE/PTP for radio backhaul); that is covered in `references/transmission/fundamentals/08-synchronization-timing.md`, and only the boundary is defined here.
- Audio and video media-clock distribution (e.g. broadcast studio timing); only noted where PAGA or CCTV interfaces touch it.

## Content basis limits

Built entirely from public IEEE/IETF/ITU-T/IEC/IRIG standards knowledge and general time-distribution design practice, not a specific past project. All numeric figures in this subsystem are illustrative; verify against the governing specification, vendor documentation and project requirements. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA, CCTV and Transmission.
