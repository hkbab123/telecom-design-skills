# Alarm Rationalisation — EEMUA 191

The method behind Stage 2 item 11 — read this when the question is "how do I actually rationalise an alarm list," not just "decide the alarm philosophy."

## The problem EEMUA 191 addresses

Left unmanaged, SCADA/DCS alarm configuration tends toward "configure everything that can be an alarm as an alarm" — every status change, every out-of-range excursion, every device fault becomes an alarm, regardless of whether it requires operator action. During a genuine upset (exactly when clear alarms matter most), this produces an **alarm flood** — hundreds of alarms per minute — that overwhelms the operator's ability to identify the handful that actually require action. EEMUA 191 is the industry's practical guide to preventing this.

## Key EEMUA 191 concepts

- **An alarm should require operator action.** If nothing needs to change in response, it's a status indication or an event-log entry, not an alarm — this single principle eliminates a large share of typical over-alarming.
- **Alarm priority classes** — typically three to four levels (e.g. Emergency/Critical/High/Low), each with a defined expected operator response time, so priority is meaningful rather than decorative.
- **Target alarm rates** — EEMUA 191 publishes benchmark figures for a "manageable" steady-state alarm rate per operator per hour, and separately for a peak/flood condition — used as a design target during rationalisation, not a hard external requirement, but a widely cited industry benchmark worth stating explicitly in the Stage 2 specification.
- **Alarm rationalisation as a documented exercise** — a structured, documented review of every proposed alarm (its cause, consequence, and required operator action) before configuration, producing an alarm philosophy document and a master alarm database — not something left to whatever a contractor's engineer configures by default.

## Nuisance and duplicate alarms

Common flood contributors: alarms that chatter (rapidly toggle in and out of alarm state near a threshold — addressed with deadbands/hysteresis), and duplicate alarms (the same underlying condition alarming from multiple tags/systems) — both are things the Stage 2 alarm philosophy should explicitly require the design to avoid, and the Stage 3 commissioning process should explicitly test for.

## Why this matters for design decisions

- This is the detailed method behind Stage 2 item 11 — specifying "alarm rationalisation per EEMUA 191 principles" at tender stage, rather than leaving alarm configuration to the contractor's default, is what prevents the flood problem from being discovered only after commissioning, when it's expensive to fix.
- Alarm rationalisation intersects with the SIS boundary (Fundamentals file 07): a SIS trip should still surface as a clear, high-priority SCADA alarm (status, for operator awareness) even though SCADA has no role in causing or preventing the trip itself.

Formal reference: EEMUA 191 ("Alarm Systems — A Guide to Design, Management and Procurement") — an industry guide, not a formal international standard, but the de facto reference across the sector.
