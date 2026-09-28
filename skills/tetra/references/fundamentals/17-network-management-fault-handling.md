# Network Management & Fault/Alarm Handling

The operational visibility layer behind the SwMI (fundamentals file 02) — read this when the question is "how does anyone know the network is broken."

## What an NMS does

The **Network Management System** monitors every managed element in the SwMI — exchange, base stations, transmission links, power systems (via site monitoring hardware) — and surfaces their operational status: healthy, degraded, or failed, along with performance statistics (traffic load, blocking rate, error rates) useful for capacity planning over the network's operational life, not just fault detection.

## Alarm severity and routing

Alarms are typically categorised by severity (critical, major, minor, warning — exact taxonomy is OEM-specific) and routed to whoever needs to act: a critical exchange failure alarm needs immediate operations-centre attention; a minor performance-degradation warning might just log for later review. Designing the alarm routing/escalation policy (who gets notified, how fast, by what channel — email, SMS, NMS dashboard) is itself a requirement to capture, not something the NMS does automatically without configuration.

## Exporting to the client's own SCADA/enterprise monitoring — SNMP and the practical export question

A client that already runs a SCADA historian or an enterprise IT monitoring dashboard (Nagios, Zabbix, a proprietary NOC platform, etc.) will usually want the TETRA NMS's alarms and performance metrics to appear there too, rather than requiring operators to watch a separate TETRA-specific screen. The standard mechanism is **SNMP** (Simple Network Management Protocol) — most OEM NMS platforms can export alarms as SNMP traps (an alarm-triggered push notification) and expose performance counters via SNMP polling (the monitoring platform queries values on an interval), letting the client's existing monitoring tooling ingest TETRA network health without a bespoke integration. What to confirm with the specific OEM before assuming this "just works": which MIB (Management Information Base — the schema defining what SNMP objects/traps the device exposes) the platform implements, whether it's a vendor-proprietary MIB or a more standard one, and which specific alarms/metrics are actually mapped to SNMP output versus only visible in the OEM's own NMS UI — a platform's marketing claim of "SNMP support" doesn't guarantee every alarm a client cares about is actually exported.

## Relationship to the reliability/safety case

The MTTR (mean time to repair) figure referenced in Stage 2 item 15's availability KPIs depends directly on how fast a fault is detected and routed to the right person — an NMS with slow or poorly-routed alarming will produce a worse real-world MTTR than the equipment's raw repair time would suggest. For O&G deployments where the safety case depends on network availability, NMS alarm routing deserves the same scrutiny as the redundancy architecture itself (fundamentals file 15) — a redundant system that fails over correctly but nobody notices needs replacing has a resilience gap.

## Why this matters for design decisions

- NMS requirements (what's monitored, alarm routing, integration with the client's own operations centre/help-desk system) belong in the interfaces checklist (Stage 2 item 13) as a distinct integration point, alongside SCADA/telephony/dispatcher interfaces — worth flagging as a possible gap in the current Stage 2 sequence, which doesn't call out NMS/fault-management interfacing explicitly.
- The reliability/safety case (Stage 2 item 15, Stage 3 item 13) should account for detection-and-response time (via NMS alarm routing), not just the equipment's raw MTBF/MTTR specs, when arguing an overall availability figure.

Formal reference: no TETRA-specific standard covers NMS design — general telecom network-management practice, implemented via the OEM's own NMS product.
