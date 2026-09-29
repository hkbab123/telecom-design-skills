# Acoustic Theory — Sound Pressure Level and Speech Intelligibility

Underpins Stage 2 item 3 (acoustic design targets) and Stage 3 item 5 (detailed acoustic modelling) — read this when the question is "why is my announcement audible but nobody can understand it," a genuinely different problem from "is it loud enough."

## Sound Pressure Level (SPL) — the loudness half of the problem

**SPL**, measured in decibels (dB), is how loud a sound is at a given point. Two things drive whether an announcement is loud enough to be heard: the loudspeaker's output and its distance from the listener (SPL falls off with distance — roughly 6 dB per doubling of distance in free field), and the **ambient noise level** at the listening point (a compressor room at 95 dB(A) needs a far louder announcement than a quiet office at 45 dB(A) to be heard at all). The design target is usually expressed as a **margin above ambient noise** — e.g. "announcement SPL at least 10-15 dB above the measured ambient noise level at the furthest listener position in the zone" — not an absolute SPL figure, because what counts as "loud enough" is entirely relative to how loud the background already is.

## Speech Transmission Index (STI) — the intelligibility half, and why it's the one that actually matters

Being loud enough doesn't mean being *understandable*. **STI** (Speech Transmission Index, 0 to 1, or its simplified equivalent CIS — Common Intelligibility Scale) measures how much a room's acoustics (reverberation, echo, background noise, frequency response) degrade speech so that consonants and syllables become distinguishable or blur together. A GA evacuation instruction announced at a perfectly adequate SPL but in a highly reverberant space (a large steel-clad warehouse, a tiled station concourse) can still be functionally useless if listeners can hear that something was said without understanding what. IEC 60849 sets STI as the actual pass/fail metric for a voice-alarm system's intelligibility performance — not SPL alone. A typical target band: STI ≥ 0.5 ("fair" to "good" intelligibility) for life-safety voice alarm, though the specific value to design against should be confirmed against the governing standard and the client's fire engineer.

## What degrades STI, mechanically

- **Reverberation time (RT60)** — how long sound persists in a space after the source stops (the time for it to decay 60 dB); higher in hard-surfaced, large-volume spaces (train station halls, process plant with steel/concrete surfaces) than in spaces with sound-absorptive materials (carpeted offices, acoustic ceiling tile). Long RT60 blurs consecutive syllables into each other.
- **Background noise** — masks quieter speech components (particularly higher-frequency consonants that carry most of speech intelligibility), independent of reverberation.
- **Loudspeaker directivity and placement** — a speaker aimed so its direct sound dominates over reflected/reverberant sound at the listener improves STI; poor aiming or over-spacing lets reverberant energy dominate.

## Worked example — why "loud enough" isn't "intelligible enough"

A process area has ambient noise of 85 dB(A) and a loudspeaker delivering 100 dB(A) SPL at the listener position — a healthy 15 dB margin, comfortably audible. But the same steel-and-concrete plant structure has a long reverberation time (say RT60 of 2.5 seconds, typical of a hard-surfaced industrial space with little sound absorption), which smears consonants across the reverberant tail and can push measured STI below the 0.5 target even though SPL margin looks fine. The fix isn't simply "add a louder speaker" — it's usually more, lower-power, well-aimed speakers closer to listeners (reducing the direct-to-reverberant sound ratio each listener experiences) rather than fewer, louder ones that pump more energy into exciting the room's reverberant field.

## Why this matters for design decisions

- Stage 2 item 3's acoustic target must specify both an SPL-above-ambient margin and an STI/CIS target — an SPL-only target is an incomplete acoustic specification and will pass a survey while failing to deliver an understandable evacuation instruction.
- Stage 3 item 5's detailed acoustic model needs real ambient-noise survey data (fundamentals file — see Stage 3 item 3) and an understanding of each zone's reverberation characteristics, not just its floor area, to correctly predict loudspeaker count and placement.
- High-reverberation zones (large steel/concrete structures, tiled halls) may need a "more, smaller, closer" loudspeaker strategy rather than a "fewer, louder" one — flag this explicitly during zone-by-zone acoustic design rather than applying one loudspeaker-density rule of thumb to every zone type.

Formal reference: IEC 60849 (sound systems for emergency purposes — sets the STI/CIS intelligibility requirement); IEC 60268-16 (defines the STI measurement method itself).
