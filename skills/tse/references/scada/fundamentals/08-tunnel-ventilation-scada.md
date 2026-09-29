# Rail Tunnel-Ventilation SCADA

The technical basis for Subsystem-specific rule 4 — read this when the question is "what does tunnel-ventilation SCADA actually control," not just "decide the control philosophy."

## What tunnel-ventilation SCADA supervises

Typically: jet fans and/or axial fans (thrust or extraction, depending on the ventilation strategy), dampers, and air-quality/environmental sensors (CO, visibility/opacity, air velocity, temperature) distributed along the tunnel. The control system's job is to keep the tunnel environment within acceptable limits during normal operation and to execute a specific, pre-engineered airflow strategy during a fire/smoke event.

## Normal mode

Driven by air-quality sensor readings (CO concentration is a common primary driver, since it's a proxy for vehicle-exhaust buildup in road/rail-adjacent tunnels) — fans run at a rate proportional to measured air quality, aiming to keep pollutant levels below a defined threshold at minimum energy cost. This is a conventional closed-loop control problem, engineered like any other SCADA/DCS control loop (Fundamentals file 01/02).

## Fire/emergency mode

An entirely different control objective: not "dilute pollutants," but "establish and maintain a specific airflow direction and velocity to keep smoke away from occupants evacuating the tunnel and away from the incident location, for the arriving emergency responders." This typically means specific fans reversing or being commanded to full thrust in a coordinated pattern (not simply "all fans on") determined by the fire's location (often provided by the fire-detection/CCTV system) and the tunnel's ventilation design (which may be one-directional, bi-directional, point-extraction, or a hybrid, depending on the original tunnel ventilation engineering study).

## Why fire mode must be its own explicitly designed and tested sequence

Because the control objective inverts (mitigate ongoing low-level pollutant buildup vs actively direct a smoke plume away from people), fire mode cannot be treated as "normal mode with bigger setpoints" — it needs its own control narrative, its own logic diagram, and its own commissioning test (Subsystem-specific rule 4, and Stage 3 items 6 and 20). Getting fire-mode airflow direction wrong is a life-safety failure, not a comfort/efficiency shortfall — this is why the governing fire/life-safety code (NFPA 130 or the national/local equivalent) typically mandates specific, documented, independently reviewed fire-mode ventilation strategies rather than leaving it to control-engineer discretion.

## The trigger mechanism

Fire mode is normally triggered by the fire-detection system (linear heat detection, smoke detection, or a manual call point), not by a SCADA operator's judgement call in the moment — SCADA's role is to display the fire-mode status clearly and, where the design permits, allow an authorised operator to select among pre-engineered fire-mode scenarios (e.g. which zone is affected) rather than freely improvise fan commands during an emergency. This mirrors the SIS-independence principle from Fundamentals file 07, applied to the fire-detection interface.

## Why this matters for design decisions

- Stage 2 item 5 and Stage 3 items 5-6 exist specifically because "we'll figure out fire mode later, it's basically the same logic" is the most common and most dangerous shortcut taken on tunnel-ventilation SCADA projects.
- Confirm the governing fire/life-safety code and the tunnel's own ventilation engineering study (which determines the fire-mode strategy) as fixed inputs before writing any fire-mode control logic — this skill does not invent a generic fire-mode sequence, since it is genuinely tunnel-specific.

Formal reference: NFPA 130 (or the applicable national/local fixed-guideway transit fire/life-safety code) — always confirm the actual governing code for the project's jurisdiction.
