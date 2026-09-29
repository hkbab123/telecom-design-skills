# Power System Engineering & Battery Autonomy Calculation

The sizing method behind Stage 3 item 10 — read this when the question is "how do I actually calculate battery autonomy," not just "decide power redundancy exists."

## Why this matters more for TETRA than a typical office network

Base station sites — especially remote O&G field sites without reliable grid power, or any site where communication must survive a mains outage (safety-relevant by definition for emergency-response traffic) — need a power system sized to keep the site operational through an outage of a defined duration, not just "some batteries."

## Load calculation

Sum the site's continuous DC power draw: base station equipment, any transmission equipment (microwave radio, if used), site monitoring/NMS equipment, and any auxiliary loads (site lighting, HVAC for the equipment cabinet if applicable). This gives a total load in watts (or amps at the site's DC voltage, commonly -48V DC in telecom practice, or the OEM's specified voltage — confirm rather than assume).

## Battery autonomy formula

```
Battery capacity (Ah) = (Total load in Amps) x (Required autonomy in hours) / (Depth of discharge factor)
```

**Worked example (illustrative figures):**
- Site load: 10 A at 48V DC
- Required autonomy: 8 hours (a client-specified requirement — not a technical default)
- Depth of discharge factor: 0.8 (batteries typically shouldn't be fully discharged, to protect battery life and ensure a safety margin — this factor is a battery-technology-specific parameter, confirm with the battery/OEM datasheet)

```
Battery capacity = (10 x 8) / 0.8 = 100 Ah
```
This determines the physical battery bank size needed — a real, sourceable spec, not an assumed round number.

## Generator sizing (extended outages)

Where required autonomy exceeds what's practical with batteries alone (remote sites with long expected grid-outage durations, or sites with no grid connection at all), a backup generator sized to the site's total load (with margin, and accounting for generator start-up/transfer time — during which the battery bank must cover the gap) extends autonomy indefinitely, subject to fuel supply logistics. Fuel autonomy (how long the generator can run unattended) is itself a sizing question tied to the client's maintenance/refuelling schedule for remote sites.

## Why this matters for design decisions

- The required autonomy duration (8 hours in the example above) is a client requirement to confirm — it directly drives battery bank size and cost, and should trace back to the client's actual operational risk tolerance (how long can this site realistically be without power before it matters operationally/safety-wise), not an assumed industry-standard figure.
- Sites without grid power at all (common for isolated O&G wellheads) need generator-based (or solar/hybrid) power as the primary source, with battery autonomy sized only to bridge a generator failure/refuelling gap, not as the main power source — a materially different sizing exercise from a grid-backed site.
- This calculation, done per-site with real load figures, is what Stage 3 item 10 ("power system design per site") actually is — the Stage 3 sequence currently states it as a checklist item without this worked method.

Formal reference: general telecom power-system engineering practice — not TETRA-specific; battery depth-of-discharge and capacity figures are always battery-technology and OEM-specific.
