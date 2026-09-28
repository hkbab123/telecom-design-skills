# Network Management & Fault/Alarm Handling

The operational visibility layer behind the GSM-R core (fundamentals file 02) — read this when the question is "how does anyone know the network is broken," particularly relevant given GSM-R's safety-relevance.

## What an NMS does

Monitors every managed element — MSC/BSC/HLR core elements, BTS sites, transmission links, power systems — surfacing operational status (healthy/degraded/failed) and performance statistics (traffic load, blocking rate, handover success rate — the last being a GSM-R-specific metric worth monitoring explicitly given the <300ms handover requirement's operational importance, see handover fundamentals file).

## Alarm severity and routing — heightened stakes for GSM-R

Alarm severity taxonomy and routing follow the same general principles as any telecom NMS (critical/major/minor/warning, routed to the appropriate operations function), but the stakes are higher wherever a fault could affect ETCS-bearer traffic (data-services fundamentals file) — a critical alarm on a site carrying ETCS data needs faster, more assured routing/escalation than an equivalent alarm on a purely voice-carrying site, and this differentiated routing policy should be an explicit design decision, not a uniform alarm-handling scheme applied identically to every site regardless of traffic carried.

## Relationship to the reliability/safety case

The MTTR figure feeding into availability targets (redundancy fundamentals file) depends directly on fault-detection and alarm-routing speed — an NMS with slow or poorly-prioritised alarming produces worse real-world MTTR than equipment specs alone would suggest, and for GSM-R this connects directly into the functional-safety case (fundamentals file 19) wherever ETCS-bearer or other safety-relevant traffic is involved.

## Handover-performance monitoring specifically

Given handover is GSM-R's most safety-critical single design constraint (fundamentals file 05), an NMS that tracks handover success rate and handover-completion-time statistics (not just binary site up/down status) gives genuinely actionable early-warning of a developing coverage or parameter-tuning problem before it causes an actual dropped call — worth specifying as an explicit NMS requirement rather than assuming generic site-health monitoring is sufficient for GSM-R's particular risk profile.

## Why this matters for design decisions

- NMS requirements deserve their own line in the interfaces/requirements checklist, with explicit differentiation for sites/traffic carrying ETCS-bearer data — worth flagging as a possible gap if the current Stage 2 sequence doesn't call this out explicitly.
- Handover-performance monitoring (success rate, completion time) should be an explicit NMS capability requirement, not assumed to be covered by generic site-health alarming.
- The reliability/safety case (Stage 2/3) should account for detection-and-response time via NMS alarm routing, not just raw equipment MTBF/MTTR, mirroring the same point made in the redundancy fundamentals file.

Formal reference: no EIRENE-specific standard covers NMS design comprehensively — general telecom network-management practice, implemented via the OEM's own NMS product, with EIRENE's handover/availability requirements shaping what's worth monitoring.
