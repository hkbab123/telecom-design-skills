# Interfacing SCADA with Other Systems

The method behind Stage 2 item 13 and Stage 3 item 14 — read this when the question is "how does SCADA actually talk to the telecom/PAGA/fire systems," not just "list the interfaces."

## The interface families (matching Stage 2 item 13)

**Safety systems** — the SIS/ESD or fire-alarm boundary (Fundamentals file 07) — one-way status/alarm into SCADA as the default posture, any exception explicitly engineered and justified.

**Telecom systems** — SCADA commonly interfaces with this skill family's TETRA and GSM-R subsystems for two purposes: (a) relaying SCADA alarms/status to a dispatcher console or field radio user (e.g. a tunnel-ventilation fault alarm reaching the operations control room via the radio dispatcher's integrated console), and (b) in some designs, radio network infrastructure health (site power, transmission link status) itself being a point SCADA monitors, treating the radio network as just another supervised system. Confirm which direction(s) of integration are actually in scope — don't assume both.

**PAGA** — a common and useful interface: SCADA can trigger a pre-recorded PAGA announcement automatically based on a process condition (e.g. a tunnel-ventilation fire-mode activation automatically triggering the matching evacuation announcement, rather than relying on an operator to notice the SCADA alarm and manually trigger PAGA separately). This is a genuinely valuable cross-subsystem design point worth raising proactively when both SCADA and PAGA are in a project's scope — see the umbrella `SKILL.md` Step 2 guidance on multi-subsystem projects.

**Enterprise systems** — historian-to-MES/ERP integration (Fundamentals file 01's Level 3/4), CMMS/maintenance-management integration (SCADA fault/alarm data feeding a work-order system) — usually lower urgency than the safety and telecom interfaces, but still needs an explicit ICD if in scope.

**Other building/plant systems** — BMS (see Fundamentals file 09's SCADA/BMS boundary discussion), fire alarm (beyond just the emergency-mode trigger — general fire-alarm status), access control (e.g. correlating an access event with a SCADA alarm for incident investigation).

## What an ICD actually needs to specify

For each interface: the protocol (from Fundamentals file 03, or a different one specific to that other system — e.g. a fire panel might use a proprietary or a different open protocol than the SCADA-internal one), the exact data points crossing the interface (not "status," but the specific tag list), the direction of each data point (one-way vs bidirectional — and if bidirectional, why), and the physical/logical demarcation point and who owns each side of it (relevant when the other system has a different contractor/vendor).

## Why this matters for design decisions

- Interfaces are consistently where multi-contractor projects generate disputes (each contractor assumes the other side of the interface works a certain way) — a precise ICD, signed by both sides' owners, is what prevents this, which is why Stage 3 item 14 exists as its own deliverable rather than being folded into the general technical specification.
- The SCADA-to-PAGA automatic-trigger interface is a good example of where treating subsystems in complete isolation (this skill's default unless a project genuinely spans more than one) would miss a valuable design opportunity — flag it explicitly when both are in scope.

Formal reference: no single governing standard for interface documentation generally; the specific protocol standards referenced per interface (Fundamentals file 03 for telecom-facing protocols) and general systems-integration ICD practice.
