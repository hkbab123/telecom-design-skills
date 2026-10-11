# Testing, Commissioning and Acceptance

## Why it matters

A time system looks fine on a screen even when it is wrong. Acceptance must compare it to an independent reference and exercise the failure behaviours, otherwise the spec's accuracy claims are untested.

## Instruments

- **Reference**: a traceable source independent of the system under test (a separate GNSS reference receiver with known calibration, or a calibrated portable standard).
- **Time interval counter or oscilloscope** for pulse and IRIG outputs.
- **PTP analyser** for PTP message timing and path asymmetry.
- **NTP monitor** or reference client for consumer-side offset.

## Test sequence (draft)

1. **GNSS and antenna** — lock, satellite count, C/N0; confirm cable-delay setting by comparing the master's 1PPS output to the reference's 1PPS (`02`).
2. **Master offset** — master output versus reference over a defined period; record the maximum offset.
3. **Distribution accuracy** — at each consumer class, measure the offset (NTP offset report, PTP analyser, IRIG/1PPS on the counter) and compare to the budget (`09`).
4. **Holdover** — remove the reference (disconnect the antenna) for a defined period and measure drift against the reference; compare to the specified holdover. For long holdover specs, test a shorter period and extrapolate using the measured drift, with the client's agreement.
5. **Failover** — power-off or disconnect the primary master; measure the maximum time step seen by consumers and the outage duration (`08`).
6. **Reference recovery** — restore GNSS; confirm the master re-converges without stepping consumers beyond the agreed limit.
7. **Split-brain** — present a deliberately offset reference or peer; verify the defined resolution and alarm.
8. **Time policy** — simulate daylight-saving transition and, if the master supports it, a leap second; check every consumer family and every display (`01`, `07`).
9. **Display clocks** — walk the site; confirm agreement within the spec; confirm sync-failure indication.
10. **Monitoring** — inject each alarm condition and confirm it arrives in the control room with the right priority (`12`).
11. **Security** — confirm unauthenticated or unauthorised time sources are rejected; confirm disabled services and access controls (`14`).
12. **Legacy outputs** — IRIG-B/1PPS/serial/impulse checked with instruments, not by eye (`06`).

## Writing acceptance criteria

State each as measurable: quantity, instrument, conditions, duration, pass limit. For example, "offset of the master to the reference shall not exceed X µs over a 24-hour period with GNSS locked" is testable; "master shall be accurate" is not.

## Documentation

Keep test records, calibrations of the instruments used, configuration backups taken at the end of acceptance, and as-built cable delays.

## Common mistakes

- Testing with the system's own monitor as the reference.
- No holdover or failover test, only an "it works" check.
- Not testing the daylight-saving change before it occurs.
- Not recording the measured cable-delay corrections.
