# Site RF Engineering for Rail Corridors

The physical hardware layer behind the link budget (fundamentals file 04) — read this when the question is "what actually sits at a trackside BTS site and why it matters."

## Antenna systems

- **Directional antennas along the corridor** — trackside BTS sites overwhelmingly use directional antennas aimed along the track (rather than omnidirectional), since coverage need is linear, not area-based — this concentrates energy where it's needed and naturally reduces interference to cells further along the line, tying directly into the frequency-planning fundamentals file's interference discussion.
- **Antenna height and siting relative to the track** — trackside antenna placement needs to account for the corridor's vertical profile (cuttings, embankments, overhead structures like gantries/bridges that can obstruct or reflect signal) — a straightforward "height above ground" figure is less meaningful here than height relative to the actual track geometry it's serving.

## Combiners, duplexers and feeder loss

Same physical-hardware principles as general RF site engineering: combiners merge multiple transmit signals onto a shared antenna feed (insertion loss to include in the link budget), duplexers allow simultaneous transmit/receive on a shared antenna, and feeder cable runs introduce loss proportional to length — always sourced from actual OEM/cable datasheets for the link budget calculation, not assumed generic values.

## Site layout and access considerations specific to rail

- **Trackside access and safety** — BTS site selection and any site work needs to account for railway operational safety requirements for trackside access (possession/line-blockage requirements for construction/maintenance work near the running line) — a real project-planning constraint, not just an RF-optimal-location question; the RF-ideal site isn't automatically the operationally practical one.
- **Power availability along the corridor** — remote sections of track often lack convenient grid power access, making the power-system design (fundamentals file 16) a significant site-engineering consideration, more so than for many urban telecom deployments.
- **Co-location opportunities** — trackside sites are sometimes co-located with existing railway infrastructure (signalling equipment huts, existing utility structures) where feasible, which can reduce civil-works cost/complexity compared to a fully standalone BTS site — worth checking during the detailed site survey (Stage 3) rather than assuming a standalone site is always necessary.

## Why this matters for design decisions

- Directional, corridor-aimed antenna design is close to a default assumption for GSM-R trackside sites, unlike a general PMR/cellular deployment where omnidirectional siting is common — worth stating this explicitly rather than treating antenna type as an open decision each time.
- Trackside access/possession requirements can materially affect project timeline and site-selection feasibility — this should be scoped as early as the detailed site survey step in Stage 3, ideally flagged even earlier during Stage 2 planning if it's likely to constrain the design.
- Power availability along remote sections directly drives whether autonomous power (generator/solar, see power-system fundamentals file) is needed rather than assuming grid connection is always available.

Formal reference: general RF/telecom site-engineering practice applied to a linear rail-corridor context — not EIRENE-specific, though EIRENE's coverage/handover requirements (fundamentals files 04-05) drive the resulting site density and antenna design choices.
