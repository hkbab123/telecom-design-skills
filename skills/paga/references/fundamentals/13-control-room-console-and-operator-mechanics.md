# Control Room, Console, and Operator Mechanics

Underpins Stage 2 item 4 (system architecture — the operator-facing layer) and Stage 3 item 6 (control room detailed design) — read this for what the human-facing side of PAGA actually needs, beyond the technical distribution layer covered in earlier fundamentals files.

## What the operator console actually needs to do

The central controller (fundamentals file 01) is the technical brain of the system; the **operator console** is how a human actually uses it. At minimum, a console needs to let an operator: select which zone(s) to address (individually, by group, or all-call), trigger a pre-recorded message or speak live, see the current status of every zone (idle, PA active, GA active, fault), and — critically for GA — trigger a manual General Alarm activation without depending on the automatic F&G/ESD trigger (fundamentals file 09) being available or correctly configured. This manual-trigger capability is a genuine design requirement, not a redundant nice-to-have: automatic triggers can fail or not cover every conceivable emergency scenario, and an operator who can see or hear something wrong needs an unambiguous, fast way to initiate GA regardless.

## Zone selection interface — mapped to the real facility, not abstract labels

A console listing zones as "Zone 1, Zone 2, Zone 3..." forces an operator to memorise or look up what each number physically covers — a genuine risk under stress. Better practice maps the zone-selection interface to a facility layout (a graphical site plan with selectable zones, or at minimum descriptive zone naming tied to actual areas — "Process Area North," "Control Building," "Muster Point A") so an operator under pressure selects the right zone quickly and correctly. This is a real Stage 2/Stage 3 design decision, not a cosmetic UI preference — confirm the interface approach explicitly rather than defaulting to whatever the OEM's console ships with unreviewed.

## Redundant/backup console locations

For facilities where the primary control room could itself become unavailable during an emergency (evacuated, damaged, or simply unstaffed at the time), a **backup console location** — a second, geographically separate point from which GA can still be triggered — is worth confirming as a requirement during Stage 2 item 4, particularly for O&G facilities where the primary control room may sit inside or near the hazard area itself. This isn't universal (confirm against the client's operational philosophy and the facility's actual risk profile) but should be an explicit question asked, not an assumption made either way.

## Operator training and procedure — a boundary note

The console can be well-designed and still be used incorrectly under stress if the operator hasn't trained on it — but operator training and emergency-response procedure development are typically outside PAGA's own scope (owned by the client's operations/HSE function), even though the design should make correct use as intuitive as possible specifically to reduce that risk. Flag this boundary explicitly during handover rather than assuming training is someone else's problem without confirming it's actually addressed somewhere in the project.

## Why this matters for design decisions

- Stage 2 item 4 should specify the operator console's zone-selection interface (graphical/mapped vs abstract labels) and manual GA trigger mechanism explicitly, not defer this to whatever the OEM ships by default.
- Stage 2 item 4 should also raise the backup-console-location question explicitly for facilities where the primary control room's own availability during an emergency is a genuine concern.
- The manual GA trigger must be verified during commissioning (fundamentals file 15) as independent of the automatic F&G/ESD trigger path — testing only the automatic trigger leaves the manual path's actual functionality unverified.

Formal reference: no single standard governs console interface design specifically; IEC 60849 and EN 54-16 set the underlying system performance and reliability requirements the console must support; the client's own operational/HSE procedures govern console staffing and operator training scope.
