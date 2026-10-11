# Concept Stage — Master Clock / Time Synchronisation

Consultant-led feasibility, ahead of tender. Order-of-magnitude/parametric detail only.

1. Client hires **Consultant** for feasibility.
2. Consultant runs an **initial survey and feasibility study**: the sites that need time (stations, depots, OCC/BCC, trackside rooms, plant control rooms, substations, offshore decks), existing clocks/NTP servers and slave-clock wiring, GNSS visibility at each site (tunnels, underground, enclosed plants), and the list of subsystems that will consume time.
3. **Stakeholder requirements** gathered from operations (passenger-facing clock consistency), signalling/control, security and CCTV, IT/cybersecurity, maintenance, HSE and incident-investigation teams: accuracy per consumer (Q1b), availability expectations, who is the time authority, any safety-related consumer (Q1d), GNSS constraints (Q1c).
4. **Market RFI** to master-clock/time-server OEMs and display-clock suppliers: high-level architecture options, indicative site counts, budgetary pricing, lead times.
5. **Architecture direction** presented as options (not a final choice): NTP-only vs NTP plus PTP vs NTP plus IRIG-B/1PPS; central dual masters vs per-site GNSS; wired impulse slave clocks vs IP clocks; GNSS-only reference vs GNSS plus a terrestrial reference.
6. **Time-policy proposal** presented: UTC for logs, local time zone and daylight-saving treatment for displays, leap-second handling (`fundamentals/01-time-fundamentals-utc-gnss-traceability.md`).

- **Calculations:** consumer count by protocol; site count and display-clock quantity; rough holdover requirement from the longest credible reference outage against the tightest consumer (`fundamentals/03-oscillators-holdover.md`, parametric accuracy only); rough end-to-end accuracy check of NTP vs PTP against Q1b (`fundamentals/09-accuracy-requirements-by-consumer.md`).
- **Deliverables:** feasibility study report, stakeholder requirements register, initial high-level proposal with architecture options, budgetary price estimate, project approval package.
- **Roles:** Consultant produces; Client requests and approves; OEM/Vendor responds to RFI; no Contractor yet.
