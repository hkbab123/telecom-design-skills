# Rail-Specific Design Variations

Underpins the rail side of Stage 2/Stage 3 wherever a decision sequence written with O&G's process-plant context in mind needs adjusting for a rail station, platform, depot, or corridor context — read this as the counterpart correction to files that otherwise lean O&G-heavy (functional safety, F&G/ESD, hazardous areas).

## Why a dedicated rail-variation file matters

Several of this skill's fundamentals files (SIL/functional safety, F&G/ESD integration, hazardous-area certification) are written with O&G's specific regulatory and operational context most prominent, because that's where those concepts are most rigorously formalised. Rail PAGA is a genuinely different operating context in several concrete ways covered here — not a lesser version of the O&G case, just differently regulated and differently triggered.

## GA trigger source: fire alarm panel, not F&G/ESD

Where O&G's GA function is commonly triggered by a Fire & Gas detection or ESD system (fundamentals file 09), rail's equivalent trigger is typically the station or depot's **fire alarm control panel**, operating under building/station fire codes (often via EN 54-series fire detection equipment) rather than a process-safety F&G system. The interface mechanics (hardwired volt-free contact vs digital bus, an ICD or equivalent cause-and-effect definition) are conceptually the same as file 09 describes, but owned by the station's fire safety engineering function rather than a process-safety team — confirm this ownership explicitly rather than assuming an O&G-style F&G interface exists on a rail project.

## SIL rating: less commonly formalised, fire-code-driven instead

As flagged in fundamentals file 07, rail GA is less commonly given a formal IEC 61508/61511 SIL rating the way O&G process-safety functions typically are. Rail voice-alarm requirements are more commonly driven directly by fire code and station/building life-safety regulation (which specify required performance — intelligibility, autonomy, redundancy — directly) rather than through a risk-graph/LOPA SIL-determination process. This doesn't mean rail GA is less rigorously specified, just differently specified — confirm which regime actually governs a specific rail project rather than importing an O&G-style SIL determination process where the applicable fire code doesn't call for one.

## Train describer / passenger information system (PIS) integration

A rail-specific interface with no O&G analogue: platform PA is commonly integrated with the station's **train describer** or **passenger information system**, automatically triggering standardised next-train, delay, or platform-change announcements without manual staff intervention — this is often a routine-PA-side feature (not GA) but is frequently the single most-used function of a station PAGA system day-to-day, and its interface (typically digital, often a defined message-trigger protocol from the PIS vendor) deserves the same ICD-based rigor as any other interface (fundamentals file 14), even though it's not safety-critical the way F&G/ESD is.

## Hazardous-area applicability: usually not relevant, confirm rather than assume

Fundamentals file 12's hazardous-area certification requirements are largely an O&G/process-plant concern — most rail station, platform, and depot environments aren't classified hazardous areas. The exception is specific rail contexts involving fuel storage/handling (depot fuelling facilities) or where a rail corridor runs adjacent to or through an O&G facility — confirm explicitly per project rather than defaulting hazardous-area certification requirements onto a station environment that doesn't need them, or conversely assuming a depot fuelling area is automatically exempt without checking.

## EMC and platform/tunnel acoustic environment

Rail environments introduce their own acoustic and electromagnetic considerations distinct from a typical O&G plant: platform and tunnel acoustics (high reverberation from hard surfaces, train pass-by noise as a major and highly variable ambient-noise contributor feeding directly into fundamentals file 02's STI calculation) and railway-specific EMC requirements (EN 50121 series, governing electromagnetic compatibility between railway electrical/signalling equipment and trackside/station systems) that an O&G-context design wouldn't otherwise need to consider.

## Why this matters for design decisions

- Confirm the GA trigger source (fire alarm panel vs F&G/ESD) and its owning function explicitly at Stage 2 item 13 for every rail project — don't reuse O&G interface assumptions by default.
- Confirm whether a formal SIL determination is actually required or whether fire-code-driven performance requirements are the governing basis — this materially changes the Stage 2 item 6 and Stage 3 item 11 deliverables' scope and form.
- Train pass-by noise should be captured explicitly as a variable, high-magnitude ambient-noise input to the acoustic model (fundamentals file 02) for any platform or tunnel zone, not treated as a static ambient figure the way a steady-state plant noise level might be.

Formal reference: national/local fire and building codes (station/platform life-safety requirements); EN 54-series (fire detection equipment, where the rail fire alarm panel interface applies); EN 50121 series (railway EMC); ISO 8201-1 and IEC 60849 continue to apply for the evacuation tone and voice-alarm performance requirements as in the general case.
