# Network Topology, Bandwidth & Latency Budgeting

Read this when the question is "how do I actually size the SCADA network," not just "decide the topology."

## Topology options (see also Fundamentals file 04 for the redundancy angle)

- **Star** — every RTU/PLC site connects directly to a central point (SCADA server location); simplest, but a single central-point failure or a single damaged link isolates that site with no redundancy unless duplicated.
- **Ring** — sites connected in a loop with a ring-protection protocol; a single break anywhere reroutes traffic around the ring without isolating any site — the common choice where the sites naturally lie along a linear route (a rail line, a pipeline corridor).
- **Mesh** — multiple interconnecting paths between sites; highest resilience, highest cost/complexity — usually reserved for a small number of critical central nodes (e.g. redundant links between a primary and backup control room) rather than every field site.

## Bandwidth budgeting

SCADA telemetry traffic itself is usually modest in raw bandwidth terms (polled/report-by-exception point data, not video) — the dominant bandwidth consumers on a shared network are usually CCTV, VoIP, or other co-resident systems if the SCADA network shares physical infrastructure with them (common on rail projects, where fibre backbone is shared across telecom subsystems). Size the link for the actual traffic mix on that physical path, not SCADA telemetry in isolation, and confirm whether SCADA has a guaranteed bandwidth/priority allocation (via QoS) on a shared network rather than competing uncontrolled with other traffic.

## Latency and polling-interval interaction

Two different things are often conflated: **network latency** (how long a packet takes to cross the link — usually low, single-digit to tens of milliseconds, on a well-designed fibre/dedicated network) and **update rate** (how often a value actually changes on the operator's screen — set by the polling interval for a polled protocol like Modbus, or by how frequently a change genuinely occurs for a report-by-exception protocol like IEC 60870-5-104). A low-latency network with a slow polling interval still produces a slow-feeling SCADA display — don't assume "the network is fast" automatically means "the data is fresh."

## Why this matters for design decisions

- Stage 2 item 4 (architecture) and item 8 (protocol) decisions both feed into this file's topology/bandwidth sizing — do them in that order, not backwards.
- On a shared multi-subsystem network (SCADA sharing fibre with telecom systems covered elsewhere in this skill), confirm SCADA's QoS/priority treatment explicitly — this is exactly the kind of cross-subsystem interface point flagged in the umbrella `SKILL.md`'s Step 2 guidance.

Formal reference: general telecom/data-network engineering practice; IEC 60870-5-104 and DNP3-over-TCP specifications for the protocol-level polling/reporting behaviour referenced above.
