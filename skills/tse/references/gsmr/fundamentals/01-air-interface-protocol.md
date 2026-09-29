# Air Interface & Protocol Architecture

What GSM-R actually does at the radio/protocol level — read this when a question is "how does GSM-R work" rather than "what do I decide next."

## GSM-R is GSM, with railway-specific additions

GSM-R is built on standard **GSM/GERAN** (2G cellular) air interface — TDMA with **8 timeslots per 200 kHz carrier**, GMSK modulation (or 8-PSK for EDGE data). It is not a separate radio technology from public GSM; it's the same 3GPP GSM standard, operating on a dedicated railway frequency band, with a defined set of railway-specific features layered on top (EIRENE FRS/SRS) that public GSM networks don't implement: functional addressing, eMLPP priority/pre-emption, VGCS/VBS group calls, and a fast-handover profile tuned for train speeds.

## R-GSM 900 band

GSM-R uses a dedicated allocation within the 900 MHz band — **R-GSM 900** (an extended/railway variant of the standard E-GSM 900 band, with the specific channel numbers allocated for rail use varying by country/regulator — always confirm the actual national allocation, never assume a fixed channel range applies everywhere). Using a dedicated band (rather than sharing spectrum with public mobile operators) is a deliberate railway-safety design choice — it removes the risk of public network congestion or interference degrading safety-relevant rail communication.

## TDMA structure

- **Carrier** — 200 kHz wide, carrying 8 timeslots.
- **Timeslot** — the basic transmission unit, assigned to one logical channel (traffic or control) per frame.
- **Multiframe/superframe structure** — as in standard GSM, various multiframe structures organise control signalling (paging, system information broadcast) and traffic channels — a fixed part of the GSM standard, not railway-specific.

## Logical channels

- **Traffic channels (TCH)** — carry voice or data.
- **Control channels** — broadcast (system information), common control (paging, random access), and dedicated control (signalling during a call) — standard GSM control-channel architecture, used by GSM-R exactly as in public GSM, with the addition of railway-specific signalling (functional number registration, group call setup) riding on the same control-channel structure.

## What's actually railway-specific (EIRENE additions)

The GSM-R-specific value sits almost entirely in the network/application layer, not the air interface itself:
- **Fast handover** — a tuned handover algorithm/parameter set meeting EIRENE's <300ms handover time requirement (see the handover fundamentals file) — achieved through GSM standard handover mechanisms, but with railway-specific parameter tuning and network design (small cells, high overlap) rather than a different protocol.
- **eMLPP priority** — standard 3GPP eMLPP (enhanced Multi-Level Precedence and Pre-emption) feature, used by GSM-R with a specific EIRENE-defined priority-level scheme mapped to railway operational roles (see the eMLPP fundamentals file).
- **VGCS/VBS** — standard 3GPP group-call features (Voice Group Call Service, Voice Broadcast Service), used by GSM-R for railway operational group communication.
- **Functional addressing** — a railway-specific numbering scheme layered on top of standard GSM subscriber addressing (see the functional-numbering fundamentals file).

## Why this matters for design decisions

- Because GSM-R is standard GSM at the air-interface level, general cellular RF planning knowledge (link budget, handover theory, frequency planning) applies directly — the railway-specific design work is in tuning that standard toolkit for train speeds and safety requirements, not inventing new radio physics.
- The R-GSM 900 band allocation is a real regulatory constraint to confirm per country — never assume a channel range carries over from one railway administration to another, especially relevant for cross-border projects.
- When a client or reviewer asks "why does GSM-R need its own network instead of just using public GSM with priority," the answer is precisely the EIRENE additions above — dedicated spectrum plus the fast-handover, eMLPP, VGCS/VBS, and functional-addressing layer, none of which a public GSM network provides.

Formal reference: 3GPP GSM/GERAN specifications (air interface baseline); EIRENE FRS/SRS (railway-specific requirements layered on top).
