# Power System Design — UPS & Battery Autonomy

The method behind Stage 3 item 12 — read this when the question is "how do I actually calculate battery autonomy," not just "decide the power requirement."

## Why SCADA power design matters more than it first appears

A SCADA system that loses power at the exact moment it's needed most (a grid outage during an emergency event) is worse than no SCADA at all, because operators and contractors come to rely on it. This is why control-room and RTU/PLC-cabinet power design is a genuine engineering exercise, not a line item — especially for rail tunnel-ventilation fire mode, which is precisely the kind of event likely to coincide with wider site power disturbance.

## Load calculation

Sum the actual DC/AC power draw of every device the UPS must support — SCADA servers, engineering workstations, network switches, RTU/PLC panel power supplies, and (if within the UPS boundary) any field instrumentation power. Add a safety margin (commonly 20-25%, but state the actual project figure rather than assuming one) for future load growth and to avoid running the UPS at its rated maximum continuously.

## Worked example

A control-room UPS supports: 2x SCADA servers (300W each), 4x workstations (200W each), 1x network switch stack (150W), and 20x RTU/PLC panel PSUs (40W each, at the control-room-adjacent panels only — remote panels have their own local UPS, sized the same way per panel).

```
Load = (2 x 300) + (4 x 200) + 150 + (20 x 40)
     = 600 + 800 + 150 + 800
     = 2,350 W
```

Apply a 25% margin: `2,350 x 1.25 = 2,938 W` — round up to the next standard UPS module rating available from the shortlisted OEM (never invent the actual product rating — confirm with OEM per the umbrella Design Rules).

## Battery autonomy

Autonomy (how long the UPS runs on battery alone) is a client requirement, not a default — commonly stated in minutes for a system expected to hand over to a generator, or hours where no generator backup exists and the requirement is genuinely "ride through an extended outage." The required battery capacity (typically in Ah at the UPS's DC bus voltage) is sized from the calculated load and the target autonomy, following the UPS OEM's own sizing methodology (chemistry-specific — VRLA/lead-acid and lithium batteries have different discharge-curve characteristics) — confirm the OEM's sizing tool/table rather than estimating from a simple Ah = (load / voltage) x hours formula, which ignores discharge-curve derating.

## Generator interface

Where a generator provides longer-duration backup beyond UPS autonomy, confirm the changeover sequence explicitly: automatic transfer switch timing, and whether SCADA itself (not just the wider site) has any monitoring/control role in generator status — this is a Stage 2 item 1 scoping question (is generator monitoring part of SCADA's scope, or a separate system SCADA only receives status from).

## Why this matters for design decisions

- This is the worked method behind Stage 3 item 12 — "UPS/battery autonomy calculation" in the stage file is this calculation, done per site/panel with real load and autonomy figures.
- Remote RTU/PLC cabinets (especially O&G wellsites without grid power) often need their own independent power design (solar/battery, or a dedicated generator), sized the same way but against a very different load and autonomy profile than a control room.

Formal reference: no single governing standard specific to SCADA power sizing; general UPS/battery-system engineering practice, informed by the availability targets set in Stage 2 item 7.
