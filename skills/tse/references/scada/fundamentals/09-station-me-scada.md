# Rail Station M&E SCADA

Read this when the question is "what does station M&E SCADA actually cover, and how is it different from a BMS," not just "decide the station SCADA scope."

## Typical scope

Station mechanical & electrical SCADA typically monitors and, to a lesser extent, controls: drainage/sump pumps (critical where stations or tunnels are below grade and flood risk exists), escalator and lift status (usually status monitoring and fault alarms, since the escalator/lift's own controller handles its detailed motion control — SCADA doesn't typically drive the escalator directly), HVAC for station public and back-of-house areas, and station lighting circuits in some designs. The common thread is: these are station-availability and passenger-safety-adjacent systems, but generally lower consequence than tunnel-ventilation fire mode — reflected in a correspondingly lower (but still explicitly stated, per Stage 2 item 7) availability target.

## SCADA vs BMS — where the boundary usually sits

A Building Management System (BMS) is the more common term for HVAC/lighting/general building-services control in a purely architectural building context. On a rail project, the distinction is often organisational rather than technical: some projects run station M&E under the same SCADA system as tunnel ventilation (a unified rail-systems SCADA); others keep a separate BMS for station building services, interfaced to the main SCADA only for high-level status. Confirm explicitly at Stage 1/2 which pattern this project uses — don't assume station M&E is automatically part of the tunnel-ventilation SCADA scope, and don't assume it's automatically separate either.

## Pump control specifics

Drainage/sump pump control is usually simple (level-driven start/stop, duty/standby alternation between two or more pumps to balance wear, high-level alarm escalation) but the consequence of failure (flooding into a tunnel or below-grade station) can be operationally serious — this is a case where a functionally simple control loop still warrants a genuinely engineered redundancy and alarm-escalation design (Fundamentals file 04), not a minimal afterthought specification.

## Escalator/lift integration

SCADA typically receives status (running/stopped/fault) from the escalator/lift's own dedicated controller via a defined interface (Stage 2 item 13) rather than incorporating escalator/lift motion control itself — that control logic, and its own applicable safety standard (e.g. lift/escalator-specific codes), sits outside this SCADA skill's scope, the same way SIS design sits outside it.

## Why this matters for design decisions

- Station M&E scope is easy to under-specify at Stage 1 ("station SCADA" can mean very different things project to project) — confirm the actual system list explicitly (Stage 2 item 1) rather than assuming a standard scope.
- The BMS/SCADA organisational boundary decision affects who bids what at tender — get it settled before the technical specification is finalised, not discovered during contractor bid clarifications.

Formal reference: no single governing standard for station M&E SCADA scope specifically — governed by the project's own systems-integration philosophy plus the general SCADA standards in `standards.md`.
