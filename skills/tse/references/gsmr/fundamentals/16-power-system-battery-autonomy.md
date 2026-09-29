# Power System Engineering & Battery Autonomy Calculation

The sizing method behind trackside BTS power design — read this when the question is "how do I actually calculate battery autonomy for a trackside site," not just "decide power redundancy exists."

## Why this matters particularly for GSM-R

Remote sections of track frequently lack convenient grid power access, and — where the site carries ETCS-bearer traffic — a power failure has the same elevated consequence as any other redundancy gap discussed in the redundancy fundamentals file: potential loss of the ETCS communication bearer, not just a voice-service degradation.

## Load calculation

Sum the site's continuous DC power draw: BTS equipment, any transmission equipment (microwave radio, if used for that site — fundamentals file 14), site monitoring/NMS equipment, and auxiliary loads (site cabinet heating/cooling if applicable, especially relevant for trackside cabinets exposed to extreme temperature variation). Gives total load in watts/amps at the site's DC voltage (commonly -48V DC in telecom practice, or per OEM spec — confirm, don't assume).

## Battery autonomy formula

```
Battery capacity (Ah) = (Total load in Amps) x (Required autonomy in hours) / (Depth of discharge factor)
```

**Worked example (illustrative figures):**
- Site load: 8 A at 48V DC
- Required autonomy: 12 hours (a client/railway-administration-specified requirement, likely higher than a comparable general PMR site given GSM-R's safety-relevance — not a technical default)
- Depth of discharge factor: 0.8 (battery-technology-specific, confirm with the datasheet)

```
Battery capacity = (8 x 12) / 0.8 = 120 Ah
```

## Generator sizing for extended/no-grid sites

Where required autonomy exceeds practical battery-only sizing (very remote sections, or sites with no grid connection at all), a backup generator sized to the site's total load — accounting for start-up/transfer time the battery bank must bridge — extends autonomy, subject to fuel-supply logistics for remote trackside access (itself a real operational planning question: how often can maintenance access this specific site to refuel, given railway possession/access constraints noted in the site-RF-engineering fundamentals file).

## Why this matters for design decisions

- The required autonomy duration is a client/railway-administration requirement to confirm explicitly — likely higher than typical for sites carrying ETCS-bearer traffic, given the safety-relevance discussed throughout this file set, and should trace to the client's own risk-tolerance/safety-case position rather than an assumed industry-standard figure.
- Sites without grid power at all need generator-based or hybrid power as the primary source, with battery autonomy sized only to bridge a generator failure/refuelling gap — a materially different sizing exercise from grid-backed sites, and worth explicitly identifying which sites fall into each category during the detailed site survey.
- Refuelling/maintenance access logistics for remote trackside generator sites should be scoped alongside the technical sizing, since railway access/possession constraints (site-RF-engineering fundamentals file) can materially affect how much autonomy is practically achievable versus theoretically calculated.

Formal reference: general telecom power-system engineering practice — not EIRENE-specific; actual autonomy targets are typically set by the specific railway administration's own operational/safety requirements.
