# Application Categories, QoS and KPIs

**Technical basis for Rule 1:** application-first, bearer-agnostic design.

## Why it matters

The application list and its KPIs are the real requirement. If they are vague, the radio and core get over- or under-built and nobody can prove compliance. In a shared IP network, QoS is the mechanism that keeps a safety-relevant flow safe when a bulk video stream arrives.

## Categories (UIC-style grouping)

| Category | Examples | Character |
|---|---|---|
| **Critical** | Railway emergency calls, group calls for operations, train-control data (ETCS), driver–controller voice | Low data volume, strict latency/reliability/priority, must survive congestion |
| **Performance** | Automatic train operation data, train-to-ground video, remote diagnostics, telemetry | Higher data volume, moderate latency, quality matters but not safety-defining |
| **Business** | Passenger services, operational IT, crew applications | Best-effort, lowest priority |

The exact application lists and their KPIs are defined in the UIC FRMCS specifications; take them from the pinned baseline, not from this file.

## KPIs to capture per application

- Latency (end-to-end or access), jitter, packet loss/reliability, throughput (uplink and downlink), connection set-up time for calls, priority/pre-emption class, availability, maximum train speed, and coverage requirement (where the KPI must hold).
- How each KPI is measured and where (on-board, at the access, end to end), because the contract needs a test.

## QoS mapping

In 3GPP, flows are mapped to QoS classes (5QI in 5G, QCI in LTE) with priority and, for guaranteed-bit-rate flows, reserved resources. The standard table includes mission-critical entries such as 5QI 65 (mission-critical push-to-talk voice), 66 (non-mission-critical push-to-talk voice), 69 (mission-critical delay-sensitive signalling) and 70 (mission-critical data); check the current table in TS 23.501 for the baseline. Allocation-and-retention priority (ARP) decides who is admitted or pre-empted when the cell is full.

**Design principle:** critical flows are small. Their protection comes from priority, pre-emption and admission control, not from raw capacity. Raw capacity is sized by the performance and business flows (`07`).

## Worked example: classifying a small application set

| Application | Category | Illustrative need | QoS treatment |
|---|---|---|---|
| Emergency group call | Critical | Tens of kbps, fast set-up, highest priority | Mission-critical voice class, pre-emption allowed |
| ETCS data | Critical | Low kbps, bounded latency, high reliability | Mission-critical data class, protected |
| On-board CCTV upload | Performance | Several Mbps per train | Lower priority, rate-limited, pre-emptable |
| Passenger Wi-Fi backhaul | Business | Best-effort | Lowest priority, may use another bearer |

## Common mistakes

- A single "FRMCS KPI" for the whole network.
- Specifying throughput for critical flows (the issue is priority and latency).
- Not stating where each KPI is measured.
- Letting performance traffic share the critical class.
