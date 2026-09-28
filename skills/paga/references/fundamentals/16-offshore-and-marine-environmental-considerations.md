# Offshore and Marine Environmental Considerations

Underpins Stage 2 items 2 and 12 (equipment dimensioning/environmental rating) for offshore O&G projects specifically — read this for what changes when a PAGA design moves from an onshore plant to an offshore platform or marine vessel.

## Why offshore isn't just "onshore plus corrosion resistance"

It's tempting to treat an offshore PAGA design as the onshore design with tougher enclosures bolted on, but several aspects of the design genuinely change, not just the equipment's environmental rating:

## Marine classification society approval — a parallel certification regime

Offshore platforms and marine vessels are subject to approval from a **marine classification society** (DNV, ABS, Lloyd's Register, and others, depending on the flag state and operator) in addition to — not instead of — the hazardous-area (fundamentals file 12) and functional-safety (fundamentals file 07) requirements that already apply. Classification society rules impose their own requirements on marine electrical/electronic equipment (type approval, specific test regimes, documentation requirements) that are a genuinely separate compliance track from IEC 60079/ATEX-IECEx hazardous-area certification — equipment can be correctly hazardous-area certified and still lack the marine type approval a classification society requires, and vice versa. Confirm which classification society governs the specific project early, since it affects which certified product variants are actually usable.

## Corrosion and environmental severity

Marine/offshore atmospheres (salt spray, high humidity, temperature extremes, constant vibration from platform machinery or vessel motion) are more severe than most onshore industrial environments, driving a higher baseline IP rating expectation and corrosion-resistant material specification (marine-grade stainless steel, specific coating systems) for loudspeakers, enclosures, and cabling — even outside any classified hazardous zone, since the marine environment itself is the driving factor, not just explosion risk.

## Platform/vessel layout — smaller zones, denser equipment

Offshore platforms and vessels are typically far more compact and compartmentalised than an onshore plant of comparable process capacity, meaning PAGA zoning tends toward smaller, more numerous zones (individual modules, decks, or compartments) rather than the larger area-based zones common onshore — this affects both the acoustic design (file 02's ambient-noise and STI considerations apply per-compartment, since noise levels can vary sharply between adjacent spaces separated by a bulkhead) and the cabling/segregation design (fundamentals file 11), where routing through multiple watertight bulkheads and fire divisions introduces its own penetration-sealing requirements beyond onshore cable-tray segregation.

## Vessel-specific alarm conventions

Marine vessels commonly follow maritime-specific alarm signal conventions (general emergency alarm signal patterns defined by SOLAS and flag-state regulations) that may differ from — or need to coexist alongside — the ISO 8201-1 evacuation tone (fundamentals file 08) used in land-based/rail contexts. Confirm which alarm convention actually governs a specific vessel or platform rather than assuming ISO 8201-1 applies universally offshore.

## Why this matters for design decisions

- Stage 2 item 12 should confirm the applicable marine classification society and its specific type-approval requirements as an explicit input, separate from and in addition to the hazardous-area certification already confirmed under fundamentals file 12.
- Zoning and acoustic design for offshore/marine projects should be planned at a finer granularity (per compartment/module) than a typical onshore zone plan, reflecting the more compact, more acoustically-segmented physical layout.
- The applicable evacuation alarm signal convention (ISO 8201-1 vs a maritime-specific SOLAS-derived signal) should be confirmed explicitly per project rather than assumed — this affects the tone/message design covered in fundamentals file 08.

Formal reference: relevant marine classification society rules (DNV, ABS, Lloyd's Register, or equivalent — confirm per project and flag state); SOLAS (International Convention for the Safety of Life at Sea) for vessel alarm signal requirements; IEC 60079 and ATEX/IECEx continue to apply for hazardous-area equipment within classified zones on the platform or vessel.
