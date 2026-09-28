# Testing & Commissioning Methodology

How a GSM-R network is actually proven to work before revenue/operational service — read this when the question is "what does the test and commissioning process technically involve," not just that it's a Stage 3 deliverable.

## Factory Acceptance Test (FAT)

Equipment-level and (where practical) system-level testing performed at the OEM's facility before shipment — verifies the equipment meets its specification (functional behaviour, interfaces, performance figures) in a controlled environment before it's committed to site installation. For GSM-R, this includes core-network element testing (MSC/BSC/HLR functional behaviour, including eMLPP/VGCS/functional-addressing features specific to GSM-R — fundamentals files 07/11) and, where feasible, integration testing against a simulated ETCS bearer interface (fundamentals file 20) ahead of the more expensive/logistically complex real-RBC integration testing done later.

## Site Acceptance Test (SAT)

Post-installation, on-site testing verifying each installed element (BTS, transmission link, power system) performs correctly in its actual deployed environment — distinct from FAT because site-specific factors (actual RF environment, actual power infrastructure, actual backhaul path) can't be fully replicated in a factory setting.

## Drive/walk test — the coverage and handover verification method

A vehicle (drive test) or handheld (walk test, for station/depot areas) traverses the corridor with test equipment logging received signal strength, call quality, and — critically for GSM-R — **handover events and handover performance** (success/failure, completion time) against the <300ms EIRENE target (handover fundamentals file). This is the practical, empirical verification that the RF link budget and frequency plan (fundamentals files 04/06) actually deliver the coverage and handover performance the design predicted — design calculations are necessary but not sufficient; drive testing is what actually proves it in the field, and discrepancies between predicted and measured performance at this stage typically drive parameter tuning (handover margins, cell overlap) rather than requiring redesign of the RF plan from scratch.

## ETCS bearer-specific testing — beyond generic voice/coverage testing

Where the network carries the ETCS data bearer, testing must additionally verify the data service (GPRS/EDGE, fundamentals file 08) meets the capacity/latency/availability parameters the Euroradio/ETCS specification requires (interfacing fundamentals file 20) — this typically involves staged integration testing with the actual RBC/onboard ETCS equipment, not just generic GSM-R network testing, and is usually a distinct, more elaborate test campaign than voice-only commissioning given the safety-relevance (functional-safety fundamentals file) of getting it right.

## Interworking/cross-border testing

For a cross-border deployment, the interworking interface (cross-border-architecture fundamentals file) needs its own dedicated test campaign — call handover across the border, functional-number reachability across cores, group-call continuity — since this is genuinely new integration surface not exercised by either country's domestic testing alone, and typically requires coordinated testing across both national teams/vendors.

## Why this matters for design decisions

- Drive/walk testing isn't just a formality confirming the design — budget for a parameter-tuning iteration cycle after initial testing, since first-pass measured handover/coverage performance rarely matches predictions exactly, particularly in the more complex rail-corridor propagation environments (tunnels, cuttings — fundamentals file 04).
- Where ETCS-bearer traffic is in scope, plan a distinct, appropriately resourced ETCS-bearer test campaign involving the actual RBC/onboard equipment — this is a materially bigger undertaking than voice/coverage-only commissioning and should be scoped and scheduled as such in the project plan.
- Cross-border projects need an explicit interworking test campaign as its own line item, coordinated across both national teams — don't assume domestic testing on each side implicitly covers it.

Formal reference: EIRENE FRS/SRS (performance requirements testing must demonstrate); general telecom FAT/SAT/drive-test practice adapted to GSM-R's specific handover and ETCS-bearer verification needs.
