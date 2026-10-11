# Mission-Critical Services: MCPTT, MCData, MCVideo

## Why it matters

The railway's group calls, emergency calls and prioritisation, delivered by dedicated circuit-switched features in a legacy radio network, are delivered in FRMCS by 3GPP mission-critical services over IP. Knowing the mapping tells you what the railway keeps, what changes, and what must be re-specified.

## The service family

- **MCPTT** (mission-critical push-to-talk, 3GPP TS 22.179, 23.379) — group and private voice calls, floor control, priority and emergency handling.
- **MCData** (TS 22.282, 23.282) — short data, file distribution, IP data and data-conversation services.
- **MCVideo** (TS 22.281, 23.281) — mission-critical video, including streaming and group video.
- **Common architecture** (TS 23.280) — identity, configuration, group management and key management shared by the three.

## Service mapping from a circuit-switched railway radio (conceptual)

| Railway need | Legacy realisation | FRMCS realisation (conceptual) |
|---|---|---|
| Group voice call | Voice group call / broadcast services | MCPTT group call |
| Railway emergency call | Dedicated emergency call with area targeting | MCPTT emergency call with priority and pre-emption |
| Call priority | eMLPP levels | MCX priority plus bearer-level ARP / QoS class |
| Functional addressing (call "the driver of train X") | Functional number registered at login | Functional alias / functional identity bound to the user, managed in the service layer |
| Train-control data bearer | Circuit-switched data | IP data over a protected QoS class |
| Location-dependent addressing | Location-dependent group routing | Group membership/location-based routing in the MC service |

The mapping is conceptual; the UIC FRMCS specifications define the authoritative functional equivalences and any gaps. List explicitly which legacy features the client relies on and check each against the baseline.

## Concepts

- **Functional identity** — a role-based identity (driver of a given train, signaller of a given area) bound to a user or device at login, decoupled from the SIM. Specify the registration, de-registration and conflict-handling rules.
- **Group management** — who can create groups, affiliate and change membership dynamically, and how this ties to train position and operations.
- **Priority and pre-emption** — at two levels: the service level (who speaks, who is interrupted) and the bearer level (which flow is admitted and which is dropped). Both must be configured consistently.
- **Interworking** — in a mixed network, group calls between legacy and FRMCS users go through an interworking function (`13`).

## Design decisions

1. Which features the client relies on today and whether FRMCS provides an equivalent in the pinned baseline.
2. Identity and addressing plan (functional aliases, groups, numbering).
3. Priority scheme across both service and bearer levels.
4. Dispatcher/console integration (`18`).

## Common mistakes

- Assuming every legacy feature has a one-to-one equivalent.
- Configuring service priority and bearer priority independently.
- Leaving functional-identity conflict handling undefined.
