# Data Services (GPRS/EDGE and the ETCS Relationship)

What "data bearer" means technically for GSM-R, and how it relates to (but is distinct from) train signalling.

## GPRS/EDGE over GSM-R

GSM-R can carry packet data using standard 3GPP **GPRS** (and its enhancement **EDGE**) — the same packet-data technology used in public 2G/2.5G networks, layered onto the GSM-R air interface and core exactly as in a public network, with no railway-specific modification to the data-bearer technology itself. Throughput is modest by modern standards (well below LTE/broadband), suited to low-to-moderate-bandwidth applications, not high-volume data.

## The ETCS relationship — important to get right

**ETCS (European Train Control System)** is the European train-signalling/control system — a completely separate system from GSM-R in terms of what it does (it determines train movement authority and speed supervision), but in many deployments **ETCS uses GSM-R's GPRS/EDGE data bearer as its communication channel** to exchange movement-authority and train-position data between the train and the trackside control system. This is the single most important distinction to get right when discussing GSM-R "data services":

- GSM-R **is not** the signalling system — it doesn't decide movement authority or speed limits.
- GSM-R **carries the data** that the ETCS signalling system uses to communicate, when the specific ETCS implementation (Level 2/3, depending on deployment) relies on a radio bearer rather than trackside signalling equipment alone.
- This is precisely why GSM-R's reliability, handover performance (fundamentals file 05), and availability targets are held to such a high standard — a failure of the GSM-R data bearer can directly affect the ETCS system's ability to communicate movement-authority updates, even though GSM-R itself performs no signalling logic.

## Voice data services vs the ETCS bearer

Voice group calls, functional-number voice traffic, and general operational data (non-ETCS) share the same GSM-R network infrastructure as any ETCS data traffic, but are logically and often physically distinguished at the network-planning level (dedicated capacity/priority treatment for ETCS-bearer traffic is common, given its higher criticality) — capacity and priority planning (Stage 2's traffic dimensioning and eMLPP design) needs to explicitly account for ETCS data bearer traffic as its own traffic class, not fold it into general voice/data capacity planning as an afterthought.

## Why this matters for design decisions

- Always clarify early in a project whether ETCS Level 2/3 is in scope and relies on the GSM-R data bearer — this changes the criticality, capacity-planning, and testing requirements for the data-services portion of the design substantially compared to a GSM-R network carrying only voice and non-safety operational data.
- Never describe GSM-R as "the signalling system" in a technical document — it's the communication bearer some signalling systems (specifically ETCS Level 2/3, where deployed) rely on; conflating the two misrepresents both systems' actual scope and responsibility.
- If ETCS data-bearer traffic is in scope, its capacity/priority/availability requirements should be sourced from the ETCS system's own specification (a separate discipline/document set from GSM-R's own EIRENE specs) — not assumed or invented within the GSM-R design.

Formal reference: 3GPP GPRS/EDGE specifications (data bearer technology); UNISIG/ERTMS specifications (ETCS, the signalling system that may use this bearer — outside this skill's scope, referenced only for the interface boundary).
