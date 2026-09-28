# Functional Safety Technical Basis (EN 50126 RAMS, SIL/THR concepts)

The safety-engineering vocabulary and reasoning behind why GSM-R design decisions keep tracing back to "the safety case" throughout this file set — read this when the question is "what does that actually mean, technically."

## RAMS — the framework railway safety engineering uses

EN 50126 defines Reliability, Availability, Maintainability, Safety (RAMS) as a single integrated engineering discipline for railway systems — not four separate concerns. For GSM-R, this matters wherever the network carries or affects safety-relevant functions (principally the ETCS data bearer, see data-services fundamentals file, and voice communication used for movement authority/emergency procedures):
- **Reliability** — probability the system performs its function without failure over a stated period (feeds MTBF figures referenced in the redundancy fundamentals file).
- **Availability** — proportion of time the system is actually able to perform its function (combines reliability and maintainability — the redundancy/failover fundamentals file's "availability target" discussion is this RAMS element in practice).
- **Maintainability** — how quickly/easily the system can be restored after failure (MTTR, feeds directly into availability).
- **Safety** — freedom from unacceptable risk of harm — the element that brings in SIL/THR below.

## SIL and THR — what they actually quantify

**Safety Integrity Level (SIL)**, from IEC 61508 (the general functional-safety standard EN 50126/50129 draw from for railway application), is a discrete rating (SIL 1 lowest to SIL 4 highest) expressing how reliably a system must perform its safety function — expressed as a target failure rate band (e.g. dangerous failures per hour) that the system's design and evidence must demonstrate it meets.

**Tolerable Hazard Rate (THR)** is the railway-signalling-specific expression of this same idea — the maximum acceptable rate of a specific hazardous event (e.g. "loss of the ETCS communication bearer during a movement authority") that the design must be shown to meet or beat, usually derived from a system-level risk assessment done by the signalling/ETCS authority, not by the GSM-R designer independently.

## Where GSM-R actually sits in this picture — an honest boundary

GSM-R itself is **not typically assigned its own SIL rating as a communication bearer** — ETCS is the safety-related application, and it is designed to tolerate certain classes of bearer failure (timeouts, message loss) through its own safety mechanisms (e.g. cyclic safety-relevant messages, sequence numbering, session timeout to a safe state) rather than relying on the bearer itself being intrinsically fail-safe. This is an important nuance: **GSM-R's job is to meet defined availability/reliability/latency targets that ETCS's own safety architecture is designed around — not to independently hold a SIL rating** — confirm this framing (and the actual bearer performance requirements ETCS expects) against the specific ETCS system specification and the railway administration's safety case documentation for the project, since the precise allocation of responsibility is a project-specific safety-case matter, not a universal constant.

## Practical implication for the GSM-R design process

Whatever availability, redundancy, MTTR, and handover-performance targets appear in Stage 2/3 of this skill's sequence are not arbitrary telecom-industry defaults where ETCS-bearer traffic is in scope — they should trace to (or at minimum not contradict) figures the railway administration's safety case has derived for the GSM-R bearer's contribution to overall ETCS system safety. Where this traceability isn't available to the designer, that's worth flagging as an open item rather than assuming generic telecom-industry availability figures are automatically safety-case-acceptable.

## Why this matters for design decisions

- Availability, redundancy, and handover-performance targets discussed elsewhere in this file set (redundancy, handover, NMS fundamentals files) should be checked for traceability to the project's actual safety case / THR allocation, not treated as independently-chosen telecom design targets.
- The precise safety responsibility boundary between GSM-R (bearer) and ETCS (safety application) is a project-specific safety-case matter — state this as an open confirmation item with the client/signalling authority rather than asserting a fixed universal allocation.
- This file gives the vocabulary (RAMS, SIL, THR) needed to have that conversation credibly with a signalling/safety engineer, not a substitute for the actual project safety case.

Formal reference: EN 50126 (RAMS), EN 50129 (safety-related electronic systems for signalling), IEC 61508 (general functional safety, the parent standard EN 50126/50129 draw from) — consult the project's ETCS system specification and safety case for the actual bearer-performance allocation.
