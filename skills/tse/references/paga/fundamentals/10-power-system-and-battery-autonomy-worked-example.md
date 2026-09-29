# Power System and Battery Autonomy — Worked Example

Underpins Stage 2 item 10 (power system and battery autonomy) and Stage 3 item 9 (power system detailed design) — read this for the actual calculation method, and why GA's autonomy target tends to be longer than a typical comms system's.

## Why GA needs longer battery autonomy than routine PA

A mains-power failure can itself be part of, or coincide with, the emergency event a GA system exists to respond to (a plant upset causing both a process incident and a power disturbance; a fire damaging electrical supply). The evacuation function specifically must keep working through exactly this scenario — which is why fire codes commonly mandate a materially longer UPS/battery autonomy target for the GA function than a "nice to have" backup would provide for routine PA-only equipment. The actual required duration is fire-code- and jurisdiction-specific (confirm per project — this is explicitly not a fixed universal figure), but is typically framed in terms of hours of standby capability plus a shorter period of full-alarm operation, not just minutes.

## The two load states a battery calculation must cover

- **Standby/quiescent load** — the power the system draws sitting idle, monitoring for faults and awaiting a trigger (controller, supervision circuitry, amplifiers in idle state) — this is the load the battery must sustain for the bulk of the required autonomy period.
- **Full-alarm load** — the much higher power draw when every amplifier is driving every loudspeaker line at full output during an actual GA event — this only needs to be sustained for a shorter period (the fire code's stated alarm-operation duration), but must be calculated against the system's actual worst-case simultaneous-activation scenario (all zones alarming at once), not an average or partial-activation assumption.

## Worked example

A facility's GA system has a standby load of 150W and a full-alarm load of 1.8kW (every amplifier driving every zone simultaneously — the worst-case design assumption). The applicable fire code requires 24 hours of standby capability followed by 30 minutes of full-alarm operation (illustrative figures — confirm the actual mandated duration against the governing code for the project).

- Standby energy requirement: 150W × 24h = 3.6 kWh
- Full-alarm energy requirement: 1.8kW × 0.5h = 0.9 kWh
- Total energy requirement: 4.5 kWh

Battery capacity is then sized from this total energy figure against the battery technology's usable depth-of-discharge (batteries generally shouldn't be discharged to 100% of rated capacity without shortening their service life — confirm the applicable depth-of-discharge derating factor with the OEM) and the system's DC bus voltage, giving the actual battery Ah rating to specify. This is a genuine per-project calculation using the actual connected-load figures from Stage 3's finalised equipment list (Stage 3 item 8) — not something to estimate from a rule of thumb once real amplifier/zone counts are known.

## Generator sizing — for sites beyond battery-only autonomy

Remote O&G field sites without grid connection, or sites where the required autonomy period exceeds what's practical to battery-back economically, need generator backup sized against the same full-alarm worst-case load figure, with its own separate fuel-autonomy and automatic-start requirement — a distinct design exercise from battery sizing, addressed explicitly rather than assumed covered by "there's a generator on site" without confirming it's actually sized for and wired to the GA load.

## Why this matters for design decisions

- Stage 2 item 10 should state the actual fire-code-mandated autonomy duration explicitly (standby + full-alarm periods) as a client/regulatory input to confirm, not an assumed figure — never carry a duration over unchanged from a different jurisdiction or a different subsystem's typical comms-battery target.
- Stage 3 item 9's detailed calculation must use the real standby and full-alarm load figures from the finalised equipment list, with an explicit depth-of-discharge derating and DC bus voltage assumption stated in the calculation, not left implicit.
- Where a remote site depends on generator backup beyond battery autonomy, confirm the generator is actually sized for and interfaced to the GA load specifically, not assumed adequate because a generator exists on site for other purposes.

Formal reference: no single international standard sets the autonomy duration figure itself — this is set by the applicable national/local fire code; IEC 60849 sets the general reliability-under-power-failure performance expectation the sized system must meet.
