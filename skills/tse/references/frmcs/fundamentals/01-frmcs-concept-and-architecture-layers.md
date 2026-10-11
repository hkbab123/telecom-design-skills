# FRMCS Concept and Architecture Layers

## Why it matters

FRMCS is not "GSM-R on 5G". It is a layered service platform: applications ask for communication with defined needs, a service layer provides it, and one or more transport bearers carry it. Understanding the layers is what lets you design for the application KPIs (Rule 1) instead of for a radio.

## The layers (conceptual)

1. **Applications** — what the railway wants to do: voice and group calls, train control data, train-to-ground video, diagnostics, passenger and operational data. Grouped as critical, performance and business (`02`).
2. **FRMCS service layer** — the common services that applications use: mission-critical push-to-talk, data and video services, identity and addressing (including railway functional identities), service access control, and the application-facing interface that hides the bearer details. Built on 3GPP mission-critical services (`03`).
3. **Transport layer** — one or more bearers carrying the traffic: 5G NR as the target, LTE as an early bearer, and others as options (public networks, satellite, Wi-Fi) through the on-board gateway (`11`).
4. **Trackside and on-board domains** — trackside: radio access, core, service platform, backhaul. On-board: gateway, antennas, cab and application interfaces.

## What's new compared with a circuit-switched radio

- **All-IP, packet-switched throughout.** Voice, signalling and data share an IP transport; QoS, not dedicated circuits, protects critical flows.
- **Bearer-agnostic by design.** The railway application does not need to know whether it rides on a dedicated network, a public network or another bearer; the gateway and service layer handle selection.
- **Standards from the public mobile ecosystem.** FRMCS reuses 3GPP mission-critical services and 5G, with railway-specific requirements added. That brings a larger supplier base and faster evolution, and also a moving specification (Rule 4).
- **Multi-tenant and sliceable.** One physical network can serve several services or tenants with differentiated QoS (`09`, `10`).

## Standards relationships

- UIC defines what the railway needs (URS/FRS/SRS).
- 3GPP defines the technical mechanisms (TS 22.289 and the mission-critical service specifications).
- ETSI turns railway requirements into system-level documents; ERA/EU rules decide what is mandatory for interoperability.
- CENELEC standards (EN 50126/50129/50159, TS 50701) govern safety and cybersecurity obligations.

## Common mistakes

- Treating FRMCS as a radio upgrade and designing coverage first.
- Forgetting the on-board half of the system.
- Assuming that "5G" in a tender means a railway-capable mission-critical service.
- Not recording which specification release a design assumes.
