# PAGA System Architecture and the Shared-Platform Concept

Underpins Stage 2 item 1 (zone philosophy/PA-GA split) and item 4 (system architecture) — read this when the question is "how is a PAGA system actually put together," not just "what order do we decide things in."

## One platform, two functions

A PAGA system is physically one set of amplifiers, loudspeakers, and cabling — but it delivers two functionally distinct services: **Public Address (PA)**, routine operational announcements (paging, background messaging, non-emergency instructions), and **General Alarm (GA)**, the safety-critical evacuation/alert signalling function. They share hardware because it would be wasteful to run two independent loudspeaker networks into the same building, but they do not share design rigor: GA carries functional-safety obligations (see fundamentals file 07) that PA does not. Every zone in a design should be tagged PA-only, GA-only, or both, because that tag determines which downstream requirements (supervision, redundancy, SIL) actually apply to it.

## Core architectural components

- **Central controller/matrix** — the decision-making core: routes announcements (live or pre-recorded) to the correct zones, manages priority/override logic (an emergency GA message always pre-empts a PA message — see fundamentals file 08), and interfaces with life-safety systems (fundamentals file 09).
- **Amplifier racks** — convert the controller's audio signal into the power delivered to loudspeaker lines; sized and made redundant per fundamentals file 05.
- **Zone controllers/routers** — the switching layer between the central matrix and each physical zone's loudspeaker circuit, enabling per-zone selective calling (page only the affected zone, or all-call in an emergency).
- **Loudspeaker circuits** — the physical wiring and speakers/horns in each zone, almost always run as constant-voltage lines (fundamentals file 04) rather than low-impedance direct-drive, because CV lines let many speakers share one amplifier circuit economically over long cable runs.
- **Call stations/operator consoles** — where an operator initiates a live announcement or a zone-specific page (fundamentals file 13).

## Centralised vs distributed architecture

A **centralised architecture** puts all amplification in one equipment room, with long CV-line runs out to every zone — simpler to maintain (one room to service) but creates a larger single point of failure and larger voltage-drop/cable-loss challenges over distance. A **distributed architecture** places smaller amplifier racks nearer each zone or building, shortening cable runs and containing a single amplifier failure to a smaller area, at the cost of more equipment rooms to maintain and power. Large O&G plants and multi-building rail complexes often end up distributed for exactly the reason smaller single-building deployments don't need to be — the right choice tracks site size and criticality, not a fixed default.

## Analogue constant-voltage vs digital/IP-networked audio

Traditional PAGA uses analogue constant-voltage (CV) line distribution end-to-end (fundamentals file 04). Newer systems increasingly use **digital/IP-networked audio** — audio carried as network packets to zone-local amplifier/speaker units, with the CV line only existing in the last, short run from a local amplifier to its speakers. IP-networked systems can simplify large-site cabling (reuse existing structured cabling/fibre backbone instead of dedicated long CV runs) and make zone/system status monitoring easier, but introduce network-availability and cybersecurity considerations that a purely analogue system doesn't have. Confirm with the OEM which architecture a given product line actually uses — many systems are hybrid, with CV line for legacy zones and IP-networked for new-build.

## Why this matters for design decisions

- Every zone must be explicitly tagged PA/GA/both at the outset (Stage 2 item 1) — this tag is the input every later fundamentals file (supervision, SIL, redundancy) reads to know what applies.
- Centralised vs distributed architecture (Stage 2 item 4) should be chosen against actual site size and cable-run distance, not defaulted — see the voltage-drop worked example in fundamentals file 04 for why long CV runs matter.
- If considering an IP-networked/digital architecture, flag network availability and cybersecurity as explicit design inputs, not an afterthought — the same category of concern this skill family's TETRA skill raises for IT/OT convergence.

Formal reference: no single standard defines PAGA system architecture patterns; IEC 60849 and EN 54-16 define the performance requirements the architecture must ultimately meet, not the architecture itself.
