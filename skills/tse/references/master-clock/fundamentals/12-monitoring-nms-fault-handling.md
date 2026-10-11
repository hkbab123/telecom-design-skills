# Monitoring, NMS and Fault Handling

## Why it matters

A time system fails silently: clocks keep showing a plausible time that is slightly wrong. You only find out during an investigation, when it is too late. Monitoring is how the system proves its accuracy and catches degradation first.

## What to monitor

**At the master and sub-masters**
- GNSS state: lock, satellite count, signal strength (C/N0), position-fix stability (a moving "fixed" position hints at interference).
- Source state: which reference is in use; transitions into and out of holdover; holdover elapsed time.
- Oscillator state: warm, disciplined or free-running; discipline error.
- Clock quality indicators (e.g. PTP clock class and accuracy, NTP stratum) and their changes.
- Offset between redundant masters.
- Hardware: power, temperature, fans, module health.

**At the consumers**
- Last successful sync and the offset reported by the client.
- Display-clock status (`07`).

**Independent measurement**
- An **independent monitor** that compares masters and sampled consumers against a separate reference. A system cannot reliably monitor itself against itself.

## Alarm design

- Distinguish **informational** (sat count dipped), **warning** (reference lost, running in holdover), and **critical** (holdover about to exceed accuracy budget, masters disagree).
- Alarm text should say what the consumer impact is and what the operator should do; an alarm called "GNSS fault" with no priority will be ignored.
- Integrate to the operational control room via the existing alarm path (SNMP traps, syslog or a SCADA point) and to the fault-management system.

## Trending

Trend offset and holdover drift. A slow degradation (antenna cable ageing, oscillator ageing) shows up months before a failure.

## Fault handling

1. **Triage** — is the fault in the reference (GNSS), the master, the distribution, or the consumer?
2. **Containment** — a master in suspected spoofing is removed from service so consumers do not follow it (`02`, `14`).
3. **Recovery** — restore the reference, verify before returning to service, bring consumers back without a step (`08`).
4. **Record** — log the period during which accuracy was out of budget; this matters for later investigations.

## MTTR and spares

Define repair and spares strategy for the antenna and receiver (the most failure-prone items), and keep a tested spare receiver with known cable-delay configuration.

## Common mistakes

- No alarm when the master drops into holdover.
- Monitoring only the master, not what consumers actually see.
- The monitor reading time from the same source it is checking.
- No record of the period in which time was degraded.
