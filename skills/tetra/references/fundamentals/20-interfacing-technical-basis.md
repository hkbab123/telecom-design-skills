# Interfacing Technical Basis

How TETRA actually connects to the other systems listed in Stage 2 item 13 — read this when the question is "how does the PABX/SCADA/dispatcher interface actually work," not just "list the interfaces."

## Telephony interface (PABX/PSTN gateway)

Allows TETRA users to place/receive calls to/from the conventional telephone network. Implemented via a gateway function (sometimes integrated into the exchange, sometimes a separate device) that translates between TETRA's call-control signalling and the telephony side's signalling (traditional PABX trunk signalling, or a VoIP/SIP trunk on more modern PABX systems). Dial planning (how a TETRA user dials out to a phone number, and how an inbound phone call reaches a specific TETRA user or talkgroup) is a configuration exercise on this gateway, not a TETRA-standard-defined behaviour — largely OEM/integrator-specific.

## SCADA/central alarm interface (O&G)

Two distinct patterns, worth distinguishing when scoping Stage 2 item 13:
- **TETRA carrying SCADA telemetry data** — using TETRA's packet data service (fundamentals file 08) as a bearer for low-bandwidth telemetry, subject to that service's modest throughput ceiling.
- **SCADA/alarm system triggering TETRA notifications** — e.g. a plant alarm automatically triggering an SDS message or a voice call/announcement to a specific talkgroup. This direction typically needs a purpose-built integration (the SCADA/alarm system's own alarm-management platform pushing a notification via an API or protocol gateway into the TETRA dispatcher/SDS layer) — not a standard TETRA feature, and usually the more operationally important of the two patterns for O&G emergency response.

## Dispatcher/control-room system interface

The dispatcher console (Stage 2 item 12's functional requirements) connects to the SwMI via a vendor-specific protocol/API, giving the console its talkgroup patch, priority override, and individual-call capabilities. Where the client already has a separate control-room/operations software platform (incident management, computer-aided dispatch), integrating that platform with the TETRA dispatcher function is its own interface project, typically via the OEM's published API — confirm what integration capability the chosen OEM's dispatcher platform actually exposes before assuming any specific integration is possible.

## Adjacent radio network interface

Covered at the architecture level in the SwMI fundamentals file (02) — either an ISI connection between two TETRA SwMIs, or (for a legacy analogue PMR network being phased out) a simpler patch/interconnect device allowing calls to bridge between the old and new systems during a transition period, generally without deep protocol-level integration since the old system likely isn't TETRA-standard at all.

## Why this matters for design decisions

- Each interface in Stage 2 item 13 has a genuinely different integration mechanism (gateway translation, API integration, protocol bridging) — don't treat "interfaces" as one uniform checklist item; each needs its own ICD (Stage 3 item 12) reflecting its actual mechanism.
- The SCADA/alarm integration direction (which system triggers which) should be clarified explicitly with the client early, since it changes which vendor's platform is doing the integration work.
- Dispatcher-to-control-room-platform integration capability is OEM-specific and should be checked (not assumed) before it's promised in a technical specification.

Formal reference: no single standard covers these interfaces — each is a combination of ETSI EN 300 392-3 (interworking, ISI) plus vendor-specific gateway/API documentation.
