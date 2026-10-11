# Master Clock / Time Synchronisation — Subsystem Guide

Time-of-day and time-distribution subsystem: a traceable time source (normally GNSS-disciplined), master and sub-master clocks, and the distribution that delivers one consistent time to every consumer — passenger-facing and staff clocks, control and alarm systems, video recorders, voice and announcement systems, radio and network management, enterprise IT. Covers rail (stations, depots, OCC/BCC, tunnels, trackside rooms) and oil & gas (plant control rooms, substations, pipeline stations, offshore platforms).

**Content basis:** built from public IEEE, IETF, ITU-T, IEC and IRIG standards knowledge and general time-distribution design practice, not from a specific past project. No OEM-proprietary documentation (Meinberg, Safran/Orolia, Microchip, Siemens, Honeywell, Hopf or any other vendor) is used. Treat its decision sequences as a standards-grounded starting point that still benefits from correction by a practising time-synchronisation engineer — see `CONTRIBUTING.md` in repo root. Harish may supply project-specific reference material later for a gap-fill round, same pattern as SCADA, CCTV and Transmission.

## Subsystem-specific rules (in addition to umbrella design rules)

1. **The tightest consumer sets the requirement, not the clock.** Build a consumer-by-consumer accuracy budget first. Whether NTP is enough, or PTP or IRIG-B/1PPS is needed, follows from the most demanding consumer. See `fundamentals/09-accuracy-requirements-by-consumer.md`.
2. **Time is not frequency.** The master clock delivers time-of-day traceable to UTC; the transmission network delivers frequency (and phase where radio needs it). They often share a GNSS/PRTC source but have different failure modes and acceptance tests. Define the boundary explicitly. See `fundamentals/16-interfacing-other-subsystems.md` and `transmission/fundamentals/08-synchronization-timing.md`.
3. **GNSS is a dependency, not a guarantee.** Jamming, spoofing, antenna faults, tunnels and enclosed buildings all remove it. Every design needs a stated holdover behaviour, source-quality monitoring and, for critical sites, a second independent reference. See `fundamentals/02` and `03`.
4. **One time authority.** Every system traces to the same master hierarchy. No independent free-running clocks, no consumer quietly pointing at a public internet NTP pool. Two masters that disagree (split-brain) must have a defined resolution. See `fundamentals/08-architecture-redundancy.md`.
5. **Error accumulates per hop and per cable.** Antenna cable delay, network asymmetry, switch queuing and consumer timestamp resolution all consume budget. State end-to-end accuracy at the consumer, not at the master's output. See `fundamentals/04`, `05` and `09`.
6. **Define the time policy once.** UTC vs local time for logs and displays, time zone, daylight-saving handling, leap-second handling, date/time format — across every subsystem, in the spec. See `fundamentals/01-time-fundamentals-utc-gnss-traceability.md`.
7. **The master clock is normally non-safety; safety systems must not silently depend on it.** Confirm at Tender which consumers (if any) use time for safety-related validity or timeouts. If one does, that requirement belongs in that system's safety case and the interface is specified explicitly.
8. **Vendor/component compliance is a spec-stage gate.** Same rule as CCTV and Transmission: confirm any banned-vendor-list or sovereign-sourcing restriction (this includes the choice of GNSS constellation where a client requires it) at Tender stage, before an OEM shortlist is built.

## Step 1 — Intake questions

**Q1 — Which domain?**
- **Rail** — station, platform and depot clocks, OCC/BCC, tunnels and underground stations, trackside equipment rooms, train-borne interface.
- **Oil & gas** — plant and terminal control rooms, electrical substations, pipeline stations, offshore platforms.

**Q1b — Which consumer needs the tightest time accuracy, and how tight?** (Display-only and log correlation to about a second, vs alarm/event stamping to milliseconds, vs sequence-of-events or protection to the sub-millisecond/microsecond range.) This gates protocol choice (rule 1).

**Q1c — Is GNSS reliably available at every site that needs it?** (Tunnels, underground stations, enclosed buildings, hazardous-area antenna siting, offshore structure shadowing, regions with known jamming.) This gates reference architecture (rule 3).

**Q1d — Is any consumer safety-related?** (Does any connected system use time for validity checks, timeouts or interlocking logic?) This gates rule 7.

**Q2 — Who are you representing?** Same five roles as other subsystems: **Client**, **PMC**, **Specialized Consultant**, **Contractor**, **Vendor/OEM/System Integrator**.

## Step 2 — Work the stage-specific sequence

Read the matching stage file and walk the user through the ordered decisions, checked against governing standards (`standards.md`), any stated client requirement, and outputs of the previous stage.

**When the question is conceptual, not sequential** (e.g. "why does NTP error depend on round-trip time", "how long can an OCXO hold 1 ms", "what is PTP asymmetry") — pull the matching `fundamentals/` file rather than answering from general knowledge; the reasoning and worked examples live there.

## Step 3 — Produce the deliverable

Match detail to the stage: Concept is order-of-magnitude (consumer count, site count, protocol direction, reference approach), Tender is specification-grade (technical spec, consumer accuracy matrix, time policy, compliance matrix), Engineering is detailed and vendor-sourced (architecture drawings, cable-delay and antenna schedules, distribution and VLAN plan, NTP/PTP configuration, monitoring design, FAT/SAT plan).

## Reference files

- `stage1-concept.md` — Concept stage: feasibility, consumer and site survey, reference approach, market RFI
- `stage2-tender.md` — Tender stage: technical specification decision sequence
- `stage3-engineering.md` — Engineering stage: detailed post-award design sequence
- `standards.md` — Standards this skill references (IEEE 1588, IETF NTP RFCs, ITU-T G.8271/G.8272, IRIG 200, IEC/IEEE 61850-9-3, IEC 62443)

### Fundamentals (conceptual deep-dives)

1. `01-time-fundamentals-utc-gnss-traceability.md` — UTC/TAI/GPS time, leap seconds, time vs frequency vs phase, traceability chain — basis for Rule 6.
2. `02-gnss-receivers-antennas-vulnerability.md` — constellations, timing receivers, antenna siting, cable delay, jamming/spoofing — basis for Rule 3.
3. `03-oscillators-holdover.md` — TCXO/OCXO/rubidium/caesium, holdover arithmetic, worked examples — basis for Rule 3.
4. `04-ntp-sntp.md` — stratum, root distance, SNTP vs NTP, authentication, worked error bound — basis for Rule 5.
5. `05-ptp-ieee1588.md` — grandmaster, boundary/transparent clocks, profiles, asymmetry, worked example — basis for Rule 5.
6. `06-legacy-time-distribution-irig-pps-serial-impulse.md` — IRIG-B, 1PPS, serial time strings, minute-impulse lines.
7. `07-slave-clocks-and-display-systems.md` — analogue/digital/IP clocks, failure indication, daylight-saving handling, vandal and environmental ratings.
8. `08-architecture-redundancy.md` — master/sub-master hierarchy, failover, split-brain — basis for Rule 4.
9. `09-accuracy-requirements-by-consumer.md` — consumer accuracy matrix and worked error budget — basis for Rule 1.
10. `10-rail-stations-tunnels-ocs.md` — station, depot, OCC/BCC, tunnel and train-borne considerations, incident correlation.
11. `11-og-plant-sequence-of-events-substations.md` — DCS/ESD/F&G stamping, SOE, substations, hazardous-area antenna siting, offshore, VSAT-linked sites.
12. `12-monitoring-nms-fault-handling.md` — what to monitor, offset trending, alarm integration.
13. `13-power-environment-antenna-installation.md` — UPS, antenna mounting, lightning protection, cable delay, grounding.
14. `14-cybersecurity-time-spoofing.md` — NTP/PTP/GNSS attack surface, authentication, segmentation, vendor compliance.
15. `15-testing-commissioning-acceptance.md` — offset measurement, holdover and failover tests, GNSS-loss and DST/leap tests.
16. `16-interfacing-other-subsystems.md` — ICD requirements with transmission, SCADA/DCS, signalling, CCTV, PAGA, PABX, radio, PIS, IT — basis for Rule 2.

## Status

Master Clock was added 11-Oct-26 as the seventh built subsystem, from public standards knowledge (v0.1, pending gap-fill round against Harish's own project reference material).
