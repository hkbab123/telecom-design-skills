# Constant-Voltage Line Theory and a Worked Loudspeaker-Line Example

Underpins Stage 2 item 8 (loudspeaker and amplifier-line dimensioning) and Stage 3 item 7 (loudspeaker circuit finalisation) — read this for the actual mechanics behind "how many speakers can one amplifier circuit carry, and over what distance."

## Why constant-voltage distribution exists

Driving loudspeakers directly at their native low impedance (4-8 ohms, as in a home audio system) works fine for a handful of speakers close to the amplifier, but becomes impractical at PAGA scale — dozens or hundreds of speakers spread across a large site, at varying distances, all needing to share amplifier circuits economically. **Constant-voltage (CV) line distribution** solves this: the amplifier drives the line at a fixed, standardised voltage (commonly **70V** or **100V** line, depending on regional/OEM convention — confirm which the specified equipment uses), and each loudspeaker connects via its own small step-down transformer with a selectable **tap** that sets how many watts that speaker draws from the line. Any number of speakers can share one line, each drawing only the wattage its tap is set to, as long as the sum of all taps stays within the amplifier's rated output.

## The tap-loading calculation

Each speaker's transformer tap is set to a wattage (e.g. 1W, 2W, 4W, 8W — actual available taps are product-specific, confirm with OEM). The design rule: **sum of all loudspeaker tap wattages on a line must not exceed the amplifier's rated output power for that line**, normally with a margin (commonly 20% headroom is left for future expansion or measurement tolerance — an illustrative figure to confirm against project practice, not a fixed rule).

**Worked example:** an amplifier circuit rated at 240W drives a zone with 20 loudspeakers, each tapped at 8W = 160W total tap load. That leaves 80W of headroom (33%) on the circuit — comfortably within a typical margin target, with room to add a handful more speakers later without re-amplifying the zone. If the same 20 speakers were tapped at 15W each (300W total), the circuit would be overloaded before amplifier clipping/protection even engages reliably — the fix is either lower taps (if the SPL target still permits) or splitting the zone across two amplifier circuits.

## Voltage drop over cable run — the other constraint

Long CV-line runs (a large station platform, a spread-out plant area) lose signal to cable resistance over distance — **voltage drop**. Excessive voltage drop reduces the actual SPL delivered at the far end of a line below what the tap setting assumes, silently degrading coverage at exactly the zones furthest from the amplifier room (often the areas that most need reliable coverage, since they're furthest from where an operator might otherwise be able to intervene directly). The standard mitigation is sizing cable conductor cross-section for the actual run length and load current, calculated using standard cable-resistance/voltage-drop formulas against the amplifier's line voltage (70V/100V) and the total tap current — a genuine per-project calculation using vendor cable specifications, not a rule of thumb, and one reason centralised architecture (fundamentals file 01) becomes harder to voltage-drop-justify as site size grows.

## Why this matters for design decisions

- Stage 2 item 8's amplifier/loudspeaker-line dimensioning must sum tap wattages against amplifier rated output with an explicit headroom margin, not just count speakers per zone.
- Stage 3 item 7's cable-loading finalisation must include an actual voltage-drop calculation for each real cable run length, using vendor cable specifications — a zone that "should" be covered on paper can be silently under-delivering SPL if voltage drop wasn't checked against the real distance.
- Long-distance zones (large platforms, spread-out O&G plant) are a strong signal to consider a distributed architecture (fundamentals file 01) rather than fighting voltage drop with ever-larger cable cross-sections on a centralised design.

Formal reference: no single standard defines CV-line tap-loading practice (it's standard electro-acoustic engineering method, applied against the amplifier/loudspeaker OEM's rated specifications); IEC 60268 series covers general sound-system equipment specification and measurement methods.
