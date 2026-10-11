# Network Management, Monitoring and KPIs

## Why it matters

A contract with application KPIs is only enforceable if the KPIs are measured the same way by both sides. Monitoring also detects slow degradation before it hits operations.

## Scope of network management

- **Fault management** — alarms from radio, core, service platform, backhaul, power and on-board gateways; correlation to reduce alarm floods; integration with the railway control-centre alarm system.
- **Configuration management** — parameter baselines for radio, handover, QoS and slices; software versions; change control (`20`).
- **Performance management** — counters and KPIs per cell, per application and per train.
- **Security management** — authentication failures, anomalous access, certificate and key status (`16`).
- **Subscriber/identity management** — SIM/eSIM and functional identity status.

## Measuring KPIs

| Measure | Source | Notes |
|---|---|---|
| Coverage and signal quality | Drive/ride tests; on-board measurements | Many runs, statistics, speed and conditions recorded |
| Latency and reliability | Active probes between on-board gateway and service platform; passive measurement | State the measurement points; one-way latency needs synchronised clocks (see `master-clock`) |
| Handover performance | On-board and network logs | Interruption time distribution (`08`) |
| Throughput and congestion | Network counters; probes | Per cell, per class |
| Call set-up and service quality | Service platform records; test calls | For critical voice classes |
| Availability | Fault records and probes | Defined by the contract: what counts as an outage and how it is counted |

On-board measurement across the whole fleet gives richer data than periodic drive tests; define whether the contract accepts it.

## Alarm design

Alarms should state the impact on applications and an action. Prioritise by effect on critical flows. Define what the control centre sees versus what stays in the OSS.

## Reporting

Monthly KPI reports with trends, SLA compliance, root-cause summaries, and change history. Retain raw data for investigation and for the signalling safety case (`12`).

## Common mistakes

- KPIs defined with no measurement method.
- Relying on network counters alone when the requirement is end-to-end.
- Latency measurements across unsynchronised clocks.
- Alarms with no priority or impact statement.
