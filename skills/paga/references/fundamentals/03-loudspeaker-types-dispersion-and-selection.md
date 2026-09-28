# Loudspeaker Types, Dispersion, and Selection

Underpins Stage 2 item 8 (loudspeaker and amplifier-line dimensioning) — read this when the question is "which type of speaker goes where, and why."

## The two broad categories

- **Horn loudspeakers** — a compression driver coupled to a horn-shaped acoustic waveguide, delivering high output efficiency (more SPL per watt) and a tightly controlled, directional dispersion pattern. Used wherever high ambient noise or long throw distance demands it: outdoor plant areas, process units, open yards, anywhere a cone speaker couldn't produce enough SPL economically. Trade-off: relatively poor fidelity/frequency response compared to a cone speaker — acceptable for intelligible speech (the actual requirement), not intended for music-quality reproduction.
- **Cone loudspeakers (ceiling/wall-mount)** — the familiar low-profile speaker used in offices, corridors, control rooms, and other indoor low-noise areas; better fidelity, lower output, wider (less directional) dispersion pattern. Appropriate wherever ambient noise is modest and the space is acoustically controlled enough that a horn's directionality/high output isn't needed.

## Dispersion pattern and why it drives placement, not just speaker count

A loudspeaker's **dispersion pattern** (often specified as a coverage angle, e.g. 60°, 90°, 120°) describes how its output spreads rather than beams narrowly — this interacts directly with the direct-to-reverberant sound ratio discussed in fundamentals file 02. A narrow-dispersion horn aimed precisely at a listening area delivers more of its energy as useful direct sound (helping STI) than a wide-dispersion speaker spraying sound at reflective surfaces first. Selecting dispersion angle and placement together, zone by zone, based on the zone's geometry and reverberation characteristics, is a materially different design exercise from simply computing "how many speakers to cover this floor area" from a spacing table.

## Sensitivity and efficiency

A speaker's **sensitivity** (typically expressed in dB SPL at 1 watt at 1 metre) tells you how much acoustic output it produces per electrical watt — directly feeding the constant-voltage line loading calculation in fundamentals file 04. Higher-sensitivity horn speakers deliver more SPL per watt of amplifier capacity than lower-sensitivity cone speakers, which is part of why horns dominate high-noise/long-throw applications: reaching the required SPL margin over high ambient noise with cone speakers alone would demand impractically large amplifier capacity.

## Environment-driven selection, beyond acoustic performance

- **Outdoor/weatherproof rating (IP rating)** — outdoor plant, yard, and platform speakers need an IP rating appropriate to weather exposure (rain, dust, wash-down in some process areas); indoor office/control-room speakers don't.
- **Hazardous-area certification** — where a speaker or horn sits in a classified zone (fundamentals file 12), it needs ATEX/IECEx certification as a specific certified product variant, exactly like a TETRA terminal or GSM-R equipment item — not a general "outdoor-rated" speaker assumed automatically suitable.
- **Corrosion resistance** — offshore and coastal/marine environments (fundamentals file 16) need speakers/horns with a corrosion-resistant housing (marine-grade materials/coatings), independent of and additional to their IP rating.

## Why this matters for design decisions

- Loudspeaker type selection (Stage 2 item 8) should be driven zone-by-zone by ambient noise level, throw distance, and reverberation characteristics — not a single speaker type specified project-wide.
- Dispersion angle and aiming are placement decisions, not afterthoughts — get this wrong and even a technically loud-enough system can fail its STI target (fundamentals file 02).
- Environmental requirements (IP rating, ATEX/IECEx, corrosion resistance) layer on top of acoustic selection and must each be confirmed against the specific product variant, not assumed from a general "ruggedised" label.

Formal reference: no single standard mandates loudspeaker type selection; IEC 60849/EN 54-24 govern the performance the selected loudspeaker must achieve (SPL, frequency response, reliability under fire-alarm conditions), not which physical type to choose.
