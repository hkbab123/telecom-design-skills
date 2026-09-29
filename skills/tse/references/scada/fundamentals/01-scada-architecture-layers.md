# SCADA Architecture Layers

The method behind Stage 2 item 4 — read this when the question is "where does SCADA actually sit in the plant/station architecture," not just "decide the architecture."

## The ISA-95 layer model

ISA-95 describes industrial architecture as a layered pyramid, each layer with a different job and a different update-time requirement:

- **Level 0 — the process/field itself**: sensors, actuators, motors, dampers, fans — the physical equipment.
- **Level 1 — control**: PLCs/RTUs executing the actual control logic (millisecond-to-second scan cycles).
- **Level 2 — supervisory (SCADA/HMI)**: operator screens, alarms, trending — humans supervising and occasionally intervening in what Level 1 is already doing autonomously. This is where "SCADA" as commonly understood lives.
- **Level 3 — operations management (MES/historian/CMMS)**: production/maintenance scheduling, longer-term historical data, work-order management.
- **Level 4 — enterprise (ERP)**: business planning, procurement, finance — not a control-systems concern at all.

## SCADA vs DCS — a naming distinction worth getting right

Both supervise and control industrial processes, but historically: **DCS** (Distributed Control System) implies the controllers themselves are distributed close to the process and tightly integrated with the supervisory layer by one vendor's proprietary architecture (common in large O&G plants); **SCADA** implies geographically dispersed RTUs/PLCs (often from mixed vendors) polled over a wide-area communication link by a centralised supervisory system (common in rail, pipelines, utilities, and smaller/dispersed O&G sites). The distinction has blurred with modern platforms, but it still affects two real design decisions: how much control logic executes locally (Level 1) versus how much the operator screen (Level 2) is relied on, and how tolerant the design needs to be of communication-link latency/loss between RTUs and the supervisory layer.

## Where SCADA does NOT sit

SCADA is Level 2 — supervisory. It does not sit at Level 1 (that's the PLC/RTU's job, executing without waiting for an operator) and it must never be the mechanism that implements a Safety Instrumented Function (see the SIS fundamentals file) — a SIS is architecturally independent, sitting alongside, not underneath, the SCADA/DCS control layer.

## Why this matters for design decisions

- Stage 2 item 4's architecture choice (centralised vs distributed/hierarchical) is really a choice about how the ISA-95 layers map onto real control rooms and sites — get this right before dimensioning anything else.
- The SIS-independence point here is the same one restated more fully in the SIS fundamentals file — it recurs because it is the single most common conceptual error in SCADA scoping conversations.
- Level 3/4 integration (historian to MES/ERP) is frequently added scope creep late in a project — flag explicitly whether it's in scope at Stage 1/2, not assumed.

Formal reference: ISA-95 / IEC 62264.
