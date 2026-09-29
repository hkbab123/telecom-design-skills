# Safety Instrumented Systems (SIS) vs SCADA/DCS

The technical basis for Subsystem-specific rule 1 — read this when the question is "why can't the SIS logic just live inside the SCADA/PLC," not just "confirm the interface point."

## The core distinction

**SCADA/DCS** is the *control* layer — it optimises and supervises the process, aiming to keep it running efficiently within normal operating limits. A **SIS** (Safety Instrumented System, sometimes called ESD — Emergency Shutdown — in O&G) is the *protection* layer — it exists solely to detect a hazardous condition and independently drive the process to a safe state, regardless of what the control layer is doing at the time, including if the control layer has itself failed or is the cause of the hazard.

This independence is the whole point: if the SIS shared hardware, logic, or a network path with the SCADA/DCS it's meant to protect against, a single fault could disable both the control function and the safety function simultaneously — exactly the scenario a SIS exists to prevent. This is why Subsystem-specific rule 1 insists on architectural separation, not just logical/naming separation within one system.

## SIL — Safety Integrity Level

IEC 61508/61511 define SIL 1 through SIL 4 (increasing risk-reduction requirement) for a Safety Instrumented Function (SIF). The SIL is determined by a risk assessment (often a LOPA — Layer of Protection Analysis — exercise) specific to the hazard the SIF protects against, not chosen arbitrarily. Higher SIL typically demands more redundant SIS architecture (e.g. 2-out-of-3 voting sensor arrangements), more rigorous proof-testing intervals, and tighter independence requirements from the SIS's own supporting systems.

## What SCADA is allowed to do relative to a SIS

SCADA may **monitor and display** SIS status (is the SIS healthy, has a trip occurred, what tripped it) — this is valuable operational information. SCADA must not be **in the trip decision path** (a SIS trip logic must not depend on a SCADA server, PLC, or network link being available or correct) and should not be able to **defeat or bypass** SIS action through a control command, without an explicitly engineered, access-controlled, and time-limited override mechanism that is itself part of the SIS design, not a SCADA feature.

## The rail/fire-mode parallel

Subsystem-specific rule 4 (rail tunnel-ventilation normal vs fire/emergency mode) is the same independence principle applied to a different domain: a tunnel-ventilation fire-mode trigger (from the fire-detection system) should independently command the ventilation system into its life-safety sequence, not rely on the SCADA operator noticing an alarm and manually initiating it — SCADA's role in the emergency scenario is to display what's happening and allow supervisory override where explicitly designed for it, not to be the initiating mechanism.

## Why this matters for design decisions

- This file is the "why" behind Stage 2 item 2 (define the SIS/fire-system interface early) and Stage 3 item 7 (engineer that interface in detail) — get the independence principle right conceptually before drawing the interface diagram.
- SIS/ESD detailed design (sensor voting architecture, logic solver selection, proof-test interval) is its own functional-safety engineering discipline and explicitly out of scope for this skill (see `standards.md`) — this skill covers only the SCADA side of the boundary.

Formal reference: IEC 61508 (base functional safety standard), IEC 61511 (process-industry-specific application).
