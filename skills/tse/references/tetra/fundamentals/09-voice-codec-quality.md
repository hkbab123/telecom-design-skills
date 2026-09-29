# Voice Codec & Quality

Why TETRA voice sounds and behaves the way it does — background for any "why is voice quality X" question.

## The codec

TETRA uses an **ACELP-based speech codec** (Algebraic Code-Excited Linear Prediction), operating at a low bit rate suited to fitting within one TDMA timeslot's bandwidth (see air-interface fundamentals file — 4 timeslots share a 25 kHz carrier, so each voice channel has a tightly constrained bit budget). This is a fixed characteristic of the standard, not a configurable design choice — it explains a few things engineers are often asked about:

- **Why TETRA voice doesn't sound like a phone call** — the codec is optimised for intelligibility of speech at very low bit rates in noisy environments (radio, background plant/traffic noise), not for high-fidelity audio. This is a deliberate trade-off, not a defect.
- **Why voice quality degrades in a specific way near coverage edge** — rather than voice cutting out abruptly (like an analogue FM signal fading into noise), a digital ACELP link degrades through characteristic digital artefacts (clipping, robotic-sounding dropouts) as the link approaches the receiver sensitivity threshold, then drops entirely once below it. This is relevant when interpreting field test results (see testing/commissioning fundamentals file) — "some artefacts near cell edge" during a drive test isn't necessarily a design fault, it may be expected behaviour approaching the coverage boundary.

## Voice quality vs link budget

Voice quality is fundamentally downstream of the link budget (fundamentals file 04) — there's no separate "voice quality" design lever beyond ensuring adequate signal margin at the receiver. If a client raises a voice-quality complaint, the diagnostic path is: check received signal level at the complaint location against the link budget prediction, not adjust codec settings (which aren't adjustable in the way analogue systems' deviation/squelch settings are).

## Why this matters for design decisions

- Don't over-promise "phone-quality" voice in a technical specification — set voice-quality expectations against what an ACELP-based low-bit-rate PMR codec actually delivers, which is good intelligibility for operational communication, not broadcast/telephony fidelity.
- Voice-quality complaints in the field are a link-budget/coverage diagnostic question, not a codec configuration question — this shapes how Stage 3's testing/commissioning process should investigate quality issues.

Formal reference: ETSI EN 300 395 series (speech codec for TETRA).
