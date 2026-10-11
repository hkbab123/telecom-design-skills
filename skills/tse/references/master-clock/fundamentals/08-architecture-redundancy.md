# Architecture and Redundancy

**Technical basis for Rule 4:** one time authority, with a defined answer when two masters disagree.

## Why it matters

A time system has no useful "partly correct" state: consumers need one consistent time. Redundancy that is badly designed can split the network into two disagreeing time zones, which is worse than a clean outage.

## Typical hierarchy

1. **Reference layer** — GNSS receivers (and, where used, a second non-GNSS reference).
2. **Primary and secondary master clocks** — at two physically separate locations (e.g. OCC and BCC for rail; main control room and an alternate control room for O&G), each with its own reference and oscillator.
3. **Sub-masters / site time servers** — one per station, depot, substation or plant area, so local consumers do not cross the backbone for every request and local islands keep consistent time if the backbone fails.
4. **Consumers** — NTP/PTP clients, IRIG/pulse-fed devices, display clocks.

Alternative: per-site GNSS receivers with a central supervisor, best where the backbone is long or unreliable (pipeline stations, remote sites) and each site has sky view. Trade-off: more antennas and receivers to maintain and monitor, but no dependency on distribution paths.

## Failover

- **Hot standby** with automatic switchover, not manual.
- **Priority and quality-based selection** — the preferred master is the one with the best-quality reference; a master in holdover must rank below a master locked to GNSS.
- **No time jump** — failover must not step consumers' time by more than the agreed limit; specify the maximum step and test it (`15`).
- **Recovery** — on return of the reference, converge by slewing at a limited rate rather than stepping, unless the error exceeds a stated threshold.

## Split-brain

If two masters disagree beyond a set threshold (one spoofed, one drifting, a network partition), the design must say who wins and what alarms. Common resolutions: favour the master with a verified reference and cross-check against the other and the second reference; alarm and keep the last known good until an operator decides; never let consumers silently alternate between two answers.

## Failure-mode checklist

| Failure | Expected behaviour |
|---|---|
| One antenna or receiver | Switch to second receiver or holdover, alarm |
| Both receivers at a master | Master enters holdover, ranks below the other master |
| One master | Standby takes over inside the agreed step limit |
| Backbone partition | Sub-masters run in holdover, consistent locally; re-converge without a step on recovery |
| Sub-master failure | Consumers fall back to the redundant sub-master or the primary |
| Spoofing suspected | Reference rejected, holdover, alarm, cross-check |

## Common mistakes

- Two masters in one room sharing one antenna feed.
- Auto-selection that prefers a free-running master because its priority number is lower.
- Failover that steps the time by seconds.
- A partition producing two valid but different times with no alarm.
