# Rail: Stations, Depots, OCC/BCC, Tunnels and Train-Borne Interface

## Why it matters

On a railway the time system is the thread that lets an incident be reconstructed: signalling events, SCADA alarms, CCTV footage, announcements and radio logs all need to line up. It is also the most public subsystem: every platform has clocks.

## Site types and what each needs

- **OCC / BCC** — master clocks live here (primary and secondary at separate locations, `08`); control-room displays in UTC and local time.
- **Stations** — sub-master or time server per station; platform and concourse clocks; feeds to PIS, PAGA, CCTV, SCADA, PABX, ticketing. In underground stations GNSS is absent, so the station is wholly dependent on distribution from the surface (`02`).
- **Depots and workshops** — own sub-master; GNSS at depot is usually available but expect jamming exposure from vehicle jammers; time to train-washing, maintenance and yard-control systems.
- **Trackside equipment rooms and tunnels** — small consumers (RTUs, signalling logs, radio NMS); a sub-master or a local NTP server on the transport network.
- **Viaducts / at-grade** — GNSS available but antenna siting must avoid overhead line equipment and traction substations (strong EMI and arcing).

## Train-borne interface

Confirm how train-borne systems (on-board recorders, passenger information, CCTV, radio) obtain time: from their own GNSS, from a wayside or radio source, or not at all. A train whose on-board recorder drifts will complicate an investigation. Whether the master clock has any train-borne interface at all is a project decision; do not assume it.

## Traction environment

- EN 50121 EMC series applies to trackside and station equipment; the wiring of impulse lines, IRIG feeds and antenna cables near traction cables and substations needs the same attention as signalling cables (screening, separation, bonding).
- Antennas are exposed to overhead line equipment, lightning and wind; see `13`.

## Incident-correlation example

A tunnel-ventilation alarm, a PA announcement and a CCTV recording need to be ordered correctly in an investigation. If the SCADA is NTP-synchronised to ~10 ms but the CCTV recorder is free-running on a 20 ppm crystal, it drifts ~1.7 s per day (20e-6 × 86,400) and can be minutes off after a few weeks. The master clock spec should require *every* recorder to be a time client and to *report* its sync state.

## Design checklist

1. Master at two separate locations, each with its own GNSS.
2. Sub-master per station/depot; underground stations fed via transport network.
3. Time policy applied identically to all display and logging consumers.
4. Platform-visible clocks agree within the specified tolerance (`07`).
5. Confirm safety-related use of time with signalling (Rule 7).
6. Define how time reaches wayside rooms without IP service (impulse, serial, or none).

## Common mistakes

- Station clocks synchronised from different sources than the station's CCTV and PAGA.
- Antenna on the one location with visible overhead line equipment arcing.
- Assuming underground stations have GNSS.
- Leaving train-borne time undefined.
