# ETCS, ATO and Safety Communication

**Technical basis for Rule 6:** FRMCS carries safety communication but is not the safety system.

## Why it matters

ETCS and ATO depend on the bearer's behaviour. The communication system's job is to deliver data within agreed bounds; the signalling system's safety case decides what bounds are acceptable and how to detect violations. Confusing the two causes either over-claiming (calling the radio "safety-rated") or gaps (nobody owns the communication error handling).

## Division of responsibility

- **Signalling contractor / ETCS owner** — defines the communication requirements the bearer must meet (latency, availability, connection establishment, loss handling), owns the safety case, and implements the safe-communication protocol layers and failure reactions (for example, braking on loss of connection after a timeout).
- **FRMCS contractor** — provides a bearer that meets the stated requirements, with evidence, and a defined fault/degradation reporting interface.
- **Boundary** — the interface specification (`18`) states which party handles which error type.

## Safety-related communication (EN 50159)

EN 50159 considers threats to safety-related data over open or closed transmission systems (corruption, repetition, deletion, insertion, resequencing, delay, masquerade) and defines defences at the application layer (sequence numbers, time stamps, timeouts, source/destination identifiers, feedback, identification and safety codes, cryptographic techniques). The communication network is treated as a "black channel" whose faults are detected by the end-to-end safety layer. Therefore the FRMCS bearer does not need to be a safety-integrity-level system, but it does need to behave predictably and not produce undetectable errors beyond the assumptions in the signalling safety case.

## Inputs the signalling safety case will ask for

- Latency distribution (not just an average) and its tail behaviour.
- Availability and the frequency and duration of interruptions, including handover interruptions.
- Connection set-up time and re-establishment behaviour.
- Message-ordering and duplication behaviour of the bearer.
- Failure modes and detection.
- Security assumptions (an IP-based bearer raises the question of deliberate attack).

The railway applies RAMS processes (EN 50126) and safety-related electronic system requirements (EN 50129) at the signalling-system level; the exact allocation of tolerable hazard rates to the communication path is defined by the signalling system's design, not by this subsystem.

## ATO and future data-intensive uses

Automatic train operation adds data (timetable, speed profiles, status) that needs reliability and some bandwidth. Remote or automated driving concepts add video and control data with stricter latency and uplink demands. Treat these as application entries in the KPI matrix (`02`) with their own owners, and check whether their baselines are defined yet.

## Design decisions

1. Written KPI and error-handling responsibility split with the signalling contractor.
2. QoS class and priority for the safety-related flows, and the policy under congestion.
3. Fault and degradation reporting from FRMCS to signalling.
4. Behaviour when switching between legacy and FRMCS bearers (`13`).
5. Evidence package (measurements, statistics) for the signalling safety case.

## Common mistakes

- Claiming a safety integrity level for the radio network without the system-level allocation.
- Providing averages where the safety case needs distributions.
- Leaving the handover-interruption contribution to a later stage.
- No agreed process for change control when the signalling baseline moves.
