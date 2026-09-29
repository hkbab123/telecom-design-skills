# Terminal Types & Functional-Numbering Provisioning

What actually sits in a cab and how functional numbers get assigned operationally — the practical layer behind functional addressing (fundamentals file 07).

## Terminal categories

- **Cab radio** — fixed-installed in the train driving cab, the primary GSM-R terminal for train drivers; integrates with the cab's controls (e.g. driver's emergency call button wired directly to trigger a railway emergency call at the highest eMLPP priority) and, where ETCS Level 2/3 is in scope, provides the data connection the ETCS onboard equipment uses (see data-services fundamentals file).
- **Handheld terminal** — carried by trackside/operational staff (maintenance teams, shunters, signallers where applicable) — standard GSM-R handset supporting functional-number login, group calls, and emergency calls, analogous in role to a TETRA handheld but on GSM-R's network.
- **Fixed/desk terminal** — used in signalling centres/control rooms by signallers, often integrated with the operational control system rather than used as a standalone handset.

Each terminal type has its own RF characteristics (cab radios typically have better antenna installation and more stable power than a handheld) that feed into the link budget (fundamentals file 04) — always use the correct terminal category's actual specification, not a generic assumed figure.

## Functional-number login process

Unlike a SIM-bound public mobile number, a functional number is entered by the user at login (typically the driver enters their functional number and relevant train/duty identifiers at the start of a duty), which the network then associates with that specific terminal for the duration of the login session (technically handled via the HLR/VLR mechanism described in the network-architecture fundamentals file). At logout (end of duty, or handing over to another driver), the functional number is released and can be logged into by the next relevant duty holder on a different terminal — this is precisely what allows a call addressed to "the driver of train 1234" to reach whichever physical cab radio and driver is currently on that duty.

## Why this matters for design decisions

- Terminal-count and functional-number-count planning are related but distinct quantities: the number of physical terminals needed depends on fleet size and staff headcount, while the number of functional numbers needed depends on the number of distinct operational roles/duties — worth scoping both explicitly rather than assuming a 1:1 relationship.
- The driver's emergency call button's direct wiring to trigger a top-priority eMLPP call is a real integration point between the cab radio and the train's own systems — worth flagging explicitly as an interface/integration item in the technical specification, not just assumed as an inherent terminal feature.
- Login/logout process design (how staff actually enter functional numbers operationally) is as much an operational-procedure question for the client as a technical provisioning question — worth confirming the client's operational concept for this rather than assuming a standard process.

Formal reference: EIRENE FRS/SRS (functional numbering, cab radio and emergency-call integration requirements).
