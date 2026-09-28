# Backhaul/Transmission Along the Rail Corridor

The technical characteristics behind backhaul choice for GSM-R BTS sites — read this when the question is "how do I choose backhaul technology for a trackside site."

## Why fibre is usually the default for GSM-R specifically

Unlike a general PMR deployment (where fibre availability varies a lot by site), railway corridors very often already have (or are being built with) trackside fibre infrastructure for other systems — signalling, ETCS backbone communication, station/operational systems — making fibre backhaul for GSM-R BTS sites frequently the practical default rather than a genuinely open choice, since the civil infrastructure (ducting, access) may already exist or be shared with those other systems' build. This is somewhat GSM-R-specific compared to TETRA's more varied backhaul reality, precisely because railway corridors tend to be fibre-rich environments due to signalling's own communication needs.

## Microwave and leased circuits (where fibre isn't practical)

Used at sites where trackside fibre isn't available or economical for that specific location (remote sections, or where fibre build is deferred to a later project phase) — same technical principles as general microwave/leased-circuit backhaul (line-of-sight requirement for microwave, capacity/SLA dependency for leased circuits) covered in general PMR practice, applied to individual GSM-R BTS sites rather than the whole network.

## Capacity dimensioning — the ETCS consideration

Backhaul capacity needs to cover the site's dimensioned voice traffic (Erlang-based, fundamentals file 03) plus signalling overhead plus, critically, **ETCS data bearer traffic** where in scope (fundamentals file 08) — this last element is a GSM-R-specific dimensioning input with no TETRA equivalent, and its bandwidth/latency/reliability requirements should be sourced from the ETCS system specification rather than assumed to be a minor addition to voice traffic.

## Redundancy — heightened by the safety relevance of ETCS-bearer traffic

Where GSM-R's data bearer carries ETCS Level 2/3 traffic, backhaul redundancy (protected ring/star topology, as in general transmission-redundancy practice) takes on the same elevated importance as the exchange/core redundancy discussed in the redundancy-mechanics fundamentals file — a backhaul failure isn't just a voice-service degradation in that scenario, it's a potential loss of the ETCS communication bearer, which has direct operational/safety consequences for train movement authority in the affected section.

## Why this matters for design decisions

- Check trackside fibre availability/planned-build status early (ideally during Stage 1/2 scoping) — it's often the deciding factor for backhaul choice on a GSM-R project in a way that's less certain on a general PMR project.
- ETCS data-bearer requirements (where in scope) should be sourced explicitly from the ETCS specification and treated as a distinct, higher-priority dimensioning and redundancy input, not folded into general voice-traffic backhaul planning.
- Backhaul redundancy requirements should be explicitly elevated wherever the site's traffic includes ETCS-bearer data — this is a direct consequence of the safety-relevance discussed in the data-services fundamentals file, not an independent decision.

Formal reference: general telecom transmission engineering practice; EIRENE FRS/SRS and the relevant ETCS specification set (UNISIG/ERTMS) for the ETCS-bearer-specific requirements where applicable.
