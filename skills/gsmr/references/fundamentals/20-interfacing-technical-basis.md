# Interfacing Technical Basis (ETCS/signalling, interlocking, PA systems)

The mechanics behind GSM-R's interfaces to other railway systems — read this when the question is "how does GSM-R actually connect to the signalling/interlocking/PA system, not just that it does."

## ETCS interface — the Euroradio/EIRENE-defined bearer connection

GSM-R provides the radio bearer for ETCS Level 2/3's data communication between trackside (RBC — Radio Block Centre) and onboard (ETCS onboard unit) equipment, using packet data services (GPRS/EDGE — data-services fundamentals file) carrying the Euroradio safety-layer protocol (which itself implements the safety mechanisms — sequence numbering, timeouts, cyclic messaging — that let ETCS tolerate the bearer's own imperfections, per the functional-safety fundamentals file). The GSM-R designer's interface responsibility is to deliver a bearer meeting the capacity, latency, and availability parameters the ETCS/Euroradio specification requires (fundamentals file 08's dimensioning point) — the RBC-to-onboard application-layer protocol itself is outside GSM-R's design scope, sourced from the ETCS/ERTMS specification set (UNISIG) and the specific ETCS supplier's system.

## Interlocking interface — indirect, via operational voice/data, not a direct link

GSM-R does not typically interface directly with interlocking systems (the trackside equipment controlling points/signals) — the connection is operational rather than a direct protocol link: voice communication (driver-signaller calls, emergency calls) and, where in scope, ETCS data (which itself interfaces with interlocking via the RBC, not via GSM-R directly). Confirm this boundary explicitly for the specific project — some projects may define auxiliary data interfaces (e.g. to a traffic management system) that do touch GSM-R more directly, and this should be captured in the interface requirements rather than assumed absent.

## PA/PIS and station systems interface

Where GSM-R terminal infrastructure is co-located with or shares infrastructure with station public-address/passenger-information systems (a distinct system, not part of GSM-R itself), the interface is typically at the civil/site level (shared masts, cabinets, power, backhaul — see site-RF-engineering and backhaul fundamentals files) rather than a functional protocol interface — GSM-R's role is usually confined to voice/data communication for railway operations staff, not passenger-facing PA/PIS content, though this should be confirmed against the specific project's system boundary definition since some projects do define auxiliary functional integrations.

## Dispatcher/operational systems interface

The GSM-R core's dispatcher interface (to the signaller's/controller's operational console) is how functional-number calls, group calls, and emergency calls are actually initiated/received by operational staff — this is a genuine functional interface (not just co-location), typically an OEM-specific console/API integration between the GSM-R core (MSC-level, fundamentals file 02) and the railway's operational control system, worth specifying explicitly in the interface requirements with the actual console vendor's integration capability confirmed rather than assumed generic.

## Why this matters for design decisions

- Distinguish clearly, in the interface requirements register, between genuine functional/protocol interfaces (ETCS/Euroradio bearer, dispatcher console) and civil/site-level co-location (PA/PIS, other station systems) — conflating the two leads to either missed requirements or unnecessary scope creep.
- ETCS bearer interface requirements (capacity, latency, availability) should be sourced explicitly from the ETCS/Euroradio specification and the specific ETCS supplier, not assumed generic — this is the single most consequential interface for a GSM-R project carrying ETCS traffic.
- The dispatcher/console interface is a real functional integration point deserving its own explicit requirement and OEM-compatibility confirmation, not an assumed "of course it connects" afterthought.

Formal reference: EIRENE FRS/SRS; ETCS/ERTMS specification set (UNISIG) and the Euroradio FFFIS (Form Fit Function Interface Specification) for the safety-layer protocol running over the GSM-R bearer.
