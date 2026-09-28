# Voice Codec & Quality

Why GSM-R voice sounds and behaves the way it does — background for any "why is voice quality X" question.

## The codec

GSM-R uses standard **GSM speech codecs** (Full Rate, Enhanced Full Rate, or Adaptive Multi-Rate depending on network/terminal capability — the same codec family used in public GSM networks). This is a fixed characteristic inherited from GSM-R's standard-GSM foundation (see air-interface fundamentals file), not a railway-specific codec — there is no separate "GSM-R codec."

## Why voice quality behaves the way it does

- **Digital degradation pattern** — as with any digital link, voice quality near the coverage edge or during marginal handover conditions degrades through characteristic digital artefacts (clipping, dropouts) rather than the gradual fade of an analogue system, then drops entirely below the link's operating threshold. Relevant when interpreting field test results (testing/commissioning fundamentals file) — occasional artefacts near a cell boundary during a drive test may reflect expected behaviour at the coverage/handover margin, not necessarily a design fault.
- **Handover-related quality dips** — a handover event itself, even a successful one completing within the 300ms EIRENE target, can produce a brief audible quality dip as the link retunes — this is expected GSM/GSM-R behaviour, not evidence of a handover failure, and should be distinguished from an actual dropped call during quality assessment.

## Voice quality vs link budget and handover design

As with any digital radio system, voice quality is fundamentally downstream of the link budget (fundamentals file 04) and handover performance (fundamentals file 05) — there's no separate "voice quality" lever beyond ensuring adequate signal margin and reliable handover. A voice-quality complaint's diagnostic path is: check received signal level and handover event logs at the complaint location/time against the link budget and handover-parameter design, not adjust codec settings.

## Why this matters for design decisions

- Don't over-promise "telephone-quality" voice in a technical specification — set expectations against what a standard GSM voice codec delivers for safety-relevant operational communication, which prioritises intelligibility and reliability (backed by the handover-time requirement) over audio fidelity.
- Voice-quality field complaints should be investigated as a coverage/handover diagnostic question first (checking against Stage 3's detailed link budget and handover parameter design), before considering any equipment-level codec or hardware issue.

Formal reference: 3GPP GSM speech codec specifications (Full Rate/Enhanced Full Rate/AMR) — standard GSM, not railway-specific.
