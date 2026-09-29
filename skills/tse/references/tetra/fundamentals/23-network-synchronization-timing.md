# Network Synchronization & Timing

The precision-timing layer underneath everything else in this file set — read this when the question is "how does every site agree on exactly when a timeslot starts," not just "how does a link budget close."

## Why TETRA needs precise timing at all

TETRA is a **TDMA** system (air-interface fundamentals file, 01) — multiple users share one RF carrier by taking turns in precisely-defined timeslots. Every base station's timeslot boundaries need to be accurately synchronised, both to its own internal timing and, in multi-site deployments, to neighbouring sites, or the practical consequences range from degraded handover performance up to genuine timeslot collisions at cell boundaries. **Simulcast** (fundamentals file 02) has the strictest requirement of all: multiple sites transmitting the identical signal on the identical frequency need timing synchronisation tight enough that the signals reinforce rather than destructively interfere where their coverage overlaps — an order of magnitude tighter tolerance than ordinary multi-site trunking needs.

## Timing sources

- **GPS/GNSS** — the standard primary timing source for telecom infrastructure generally, including TETRA base stations: a GPS receiver at each site derives a highly accurate time reference from the satellite constellation, cheaply and with no dependency on the transmission network.
- **SyncE (Synchronous Ethernet)** — distributes frequency (not absolute time) synchronisation over the same Ethernet links carrying data traffic, by locking the physical-layer clock — relevant where the backhaul network (fundamentals file 14) is itself Ethernet-based and can be used to distribute timing alongside data, reducing reliance on GPS at every single site.
- **PTP / IEEE 1588 (Precision Time Protocol)** — distributes both frequency and absolute time over a packet network with much higher accuracy than ordinary network time protocols, used where a site needs GPS-grade timing but GPS reception itself is unavailable or undesirable (e.g. a site with no clear sky view, or where GNSS jamming risk is a concern — see below) — the backhaul network itself becomes the timing distribution path, sourced from one or more grandmaster clocks elsewhere in the network that do have GPS reception.

## Oscillator holdover — what happens when GNSS is lost

A site's local oscillator (the actual hardware clock, disciplined by whichever timing source above is in use) doesn't stop the instant GPS/GNSS signal is lost — it continues running on its own accuracy, drifting slowly away from true time, for a period called **holdover**. How long a site can hold acceptable timing accuracy during holdover depends on the oscillator's own quality (a basic crystal oscillator holds far less accurately, for far less time, than a high-stability oscillator such as an OCXO or rubidium standard) — the **required holdover duration** is a design input the client's operational risk tolerance should set (how long could a GNSS outage plausibly last in this environment, and what timing accuracy is still tolerable at the end of that period), not assumed generically. This matters concretely in two scenarios worth naming explicitly during Stage 2 scoping:
- **Prolonged GNSS outage** — equipment failure, satellite constellation issues, or simply a site where GPS reception is naturally marginal (deep urban canyon, dense plant structure, underground).
- **GNSS jamming/interference** — an increasingly recognised risk in both rail and O&G security contexts (deliberate or incidental interference with GPS reception) — a site's holdover duration is effectively its resilience against a jamming event, and a higher-stability oscillator (at higher cost) buys more time before timing accuracy degrades below TETRA's tolerance.

## Why this matters for design decisions

- Simulcast deployments (fundamentals file 02) should specify timing synchronisation as an explicit, tightly-toleranced requirement, not assume "GPS at each site" alone is sufficient without confirming the actual tolerance the chosen OEM's simulcast implementation requires.
- Required oscillator holdover duration is a genuine design input to confirm with the client, driven by the plausible GNSS-outage/jamming risk at the actual site environment — a remote desert site with unobstructed sky view has a different risk profile than an urban tunnel portal or a site in a region with known GNSS interference activity.
- Where GPS reception is structurally unreliable at a site (deep tunnel, dense plant, jamming-prone region), PTP distribution from a grandmaster elsewhere in the network is the standard alternative to relying on that site's own GPS receiver — worth flagging explicitly rather than assuming every site has a clean GPS fix.

Formal reference: general telecom synchronization practice (ITU-T G.8261/G.8262 for SyncE, IEEE 1588 for PTP) — not TETRA-specific standards, but the accepted method any TDMA-based radio system, including TETRA, relies on for site timing.
