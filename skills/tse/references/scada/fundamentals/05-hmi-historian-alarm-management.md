# HMI, Historian & Alarm Management Basics

The method behind Stage 2 item 12 and Stage 3 item 13 — read this when the question is "what actually makes a good operator screen or historian design," not just "decide the requirement."

## HMI screen hierarchy

Good practice organises operator screens in a hierarchy, not a flat list: **overview** (whole plant/station at a glance, high-level status only), **area** (one process area/station/tunnel section, more detail), **detail/loop** (individual equipment, full parameter set). This lets an operator navigate from "something is wrong somewhere" (overview) down to "here's exactly what and where" (detail) quickly during an event — a flat, cluttered single-screen design defeats this and is a common finding in post-incident SCADA reviews.

## High-performance HMI principles (in brief)

Modern HMI design guidance (following ISA-101 and the "high-performance HMI" body of practice) favours muted, low-saturation colour palettes with colour reserved for genuine abnormal states, minimal 3D/skeuomorphic decoration, and process-representative layouts over garish, decoration-heavy screens — the goal is that an abnormal condition visually stands out precisely because the normal-state screen is deliberately understated.

## Historian

Time-series data storage for trending, reporting, and post-event analysis. Key design parameters: **scan/store rate** (how often a tag's value is recorded — not necessarily the same as the PLC scan rate; often compressed via deadband/exception reporting to avoid storing unchanged values every cycle), **retention period** (how long data is kept online vs archived — sometimes a regulatory/audit requirement, not just an operational preference), and **query/reporting access** (who can pull historian data, and through what interface — ties into Stage 2 item 13's enterprise-system interfaces).

## Alarm management (see also the EEMUA 191 fundamentals file)

An alarm should mean "an operator must take action" — not "something happened." Confusing status/event logging with alarming is the root cause of most alarm-flood problems: every status change gets configured as an alarm, and during a real event the operator is buried in hundreds of alarms per minute, unable to identify the ones that matter. Stage 2 item 11's alarm-rationalisation requirement exists specifically to prevent this at the specification stage, before a contractor configures thousands of tags however is fastest for them.

## Why this matters for design decisions

- A poorly designed HMI/alarm system doesn't fail the FAT/SAT checklist (it "works") but fails the operator during an actual event — this is why alarm rationalisation and HMI design principles are specification-stage requirements (Stage 2), not implementation details left to the contractor's discretion.
- Historian retention period is sometimes a hidden regulatory requirement (especially where SCADA data supports an incident investigation or safety-case audit trail) — confirm this explicitly rather than defaulting to "whatever the vendor's default is."

Formal reference: ISA-101 (HMI design), EEMUA 191 (alarm management — see its own fundamentals file for detail).
