# Legacy Migration & SCADA Modernisation

Read this when the question is "how do I migrate an existing SCADA/RTU estate without an outage," not just "decide the migration approach." Relevant primarily to Stage 1 item on greenfield vs brownfield, and to any Stage 2/3 sequence run against an existing system.

## Why brownfield SCADA migration is a distinct design problem

A greenfield SCADA project designs against a blank slate; a brownfield migration must additionally: inventory and understand an existing, often poorly documented system (legacy protocol, legacy tag database, sometimes undocumented control logic accumulated over years of site modifications); decide what to keep, replace, or bridge; and — critically — execute the cutover **without an unacceptable operational outage**, especially where the existing SCADA supports a safety-relevant function like tunnel ventilation that cannot simply be switched off during the transition.

## Common legacy-protocol migration pattern

Where an existing RTU estate uses a legacy or proprietary protocol not natively supported by the new SCADA platform, a **protocol gateway/converter** is a common bridging approach — translating the legacy protocol to a modern one (e.g. legacy proprietary to IEC 60870-5-104 or OPC-UA) at the RTU level, allowing the new SCADA supervisory layer to be deployed and proven before the field RTU hardware itself is replaced. This decouples the (often larger, more disruptive) field-hardware replacement programme from the (often faster to deliver) supervisory-layer modernisation.

## Phased, no-downtime cutover approach

A typical pattern: (1) deploy the new SCADA system in parallel, receiving live data from the existing field estate (via gateway or duplicate polling) but not yet issuing any control commands — purely for validation; (2) once the new system's data is verified correct against the old system over an agreed soak period, cut operator control over on a site-by-site or system-by-system basis, keeping the old system as a fallback during this window; (3) decommission the old system only after the new one has demonstrated stable operation across a full operational cycle (including, where relevant, an actual or drilled emergency-mode event). This mirrors the general principle used elsewhere in this skill family (e.g. the TETRA guide's phased cutover fundamentals file) — never cut safety-relevant control over in a single "big bang" switch without a proven fallback.

## Cloud/edge SCADA trends (brief orientation)

Newer SCADA architectures increasingly push some processing to edge devices (local analytics/logic closer to the field, reducing reliance on a central server for time-critical decisions) and use cloud-hosted historian/analytics layers for Level 3/4 functions (Fundamentals file 01) — while keeping Level 1/2 control on-premises for latency, availability, and OT-security reasons (Fundamentals file 06). Where a client raises "should this be cloud SCADA," the honest answer for the control/supervisory core is usually "the control layer should stay on-premises; cloud is a reasonable fit for historian/analytics/reporting" — confirm this trade-off explicitly rather than defaulting either way.

## Why this matters for design decisions

- Stage 1's greenfield/brownfield question isn't cosmetic — it changes the shape of nearly every subsequent Stage 2/3 decision (protocol choice is now constrained by the legacy estate, the cutover plan becomes its own major deliverable, and the compliance/risk conversation includes "how do we prove the new system before removing the old one," not just "how do we design the new system").
- A migration project without an explicit, client-approved cutover/fallback plan is a common source of unplanned outages — treat the cutover plan itself as a Stage 2/3 deliverable, not an implementation detail.

Formal reference: no single governing standard for SCADA migration methodology; general systems-integration and change-management practice, informed by the same availability/redundancy principles as Fundamentals file 04.
