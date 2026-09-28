# Evacuation Tone Standards and Message/Priority Logic

Underpins Stage 2 item 7 (message and tone design) — read this for the mechanics behind "what actually plays over the loudspeakers, in what order, and who can interrupt whom."

## Why a standardised evacuation tone exists

A distinctive, internationally recognised alert tone lets occupants immediately recognise "this is an emergency" before a single word of the following voice instruction is even parsed — critical in the first seconds of an event, and especially valuable on sites with transient or multinational occupants (a rail station, an offshore platform crew, a plant with contractors from multiple countries) who may not share a first language for the voice instruction itself. **ISO 8201-1** defines the internationally standardised evacuation tone (a specific rising/falling frequency pattern) for exactly this reason — using it rather than an ad hoc site-specific tone means occupants who've encountered it anywhere in the world recognise it here too.

## Tone vs voice message — a two-part sequence, not either/or

A well-designed GA activation typically plays the standardised **alert tone** first (to capture attention and signal "this is different from a normal PA announcement"), followed by a clear **voice instruction** (what's happening, in general terms, and what to do — evacuate via a specific route, proceed to a muster point, etc.). Tone alone tells people something's wrong without telling them what to do; voice alone risks being missed or misunderstood in the critical first seconds before attention is captured. Designing this sequence — tone duration, message content, repeat cycle — is a genuine Stage 2 deliverable, not left to be improvised by whoever's on shift when an event happens.

## Pre-recorded vs live announcement

- **Pre-recorded messages** — a message library covering anticipated scenarios (general evacuation, muster-point direction, all-clear, zone-specific instructions), professionally recorded, consistent every time, and immediately available without depending on an operator's composure or clarity of speech under stress. The standard basis for the *first* message played on GA activation.
- **Live/talk-through capability** — lets a control-room operator override the pre-recorded library with real-time instructions once the specific situation is better understood (a genuine advantage pre-recorded messages can't match for an evolving event) — but depends on an available, composed operator, and should be treated as a capability the system provides, not the sole mechanism relied on for the critical first alert.

Most designs use pre-recorded for immediate first response, with live talk-through available as the situation develops — confirm this split explicitly rather than assuming one mode covers the whole requirement.

## Priority and override logic — the rule that must never be violated

**A General Alarm/emergency announcement must always be able to pre-empt and interrupt any Public Address announcement or background audio in the affected zone — never the reverse.** This sounds obvious stated plainly, but it's a genuine system-design requirement: the controller/matrix (fundamentals file 01) needs an explicit, testable priority hierarchy (commonly something like: GA/emergency > operator live page > pre-recorded PA announcement > background music/audio) built into its routing logic, verified during commissioning (fundamentals file 15) by actually triggering a GA event during an active PA announcement and confirming the GA message takes over immediately and completely, not queued behind whatever was already playing.

## Why this matters for design decisions

- Stage 2 item 7 should specify the tone standard (ISO 8201-1 or the applicable national equivalent), the tone-then-voice sequence structure, and the pre-recorded message library scope explicitly — not leave message content design to be improvised during commissioning.
- The priority/override hierarchy should be written down as an explicit, numbered rule set and tested as its own commissioning item (Stage 3 item 18), since a priority-logic failure is invisible during normal operation and only surfaces during an actual emergency if untested.
- If live talk-through is provided, confirm the operator training/procedure for using it under stress is addressed somewhere in the project (even if outside this skill's direct scope) — the technical capability alone doesn't guarantee effective use in a real event.

Formal reference: ISO 8201-1 (Audible emergency evacuation signal — the international standardised tone); IEC 60849 (sets the broader performance requirements for voice-alarm message delivery and priority handling).
