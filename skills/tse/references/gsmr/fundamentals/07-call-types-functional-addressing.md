# Call Types & Functional Addressing

The mechanics behind GSM-R's VGCS/VBS group calls and functional numbering — read this when the question is "how does a group call actually work" or "what is functional addressing," not just "decide the call types needed."

## Functional addressing — the core GSM-R concept

Unlike a normal mobile phone number (tied to a SIM card/subscriber), a GSM-R **functional number** is tied to a **role or duty** (e.g. "driver of train 1234," "signaller for control area X," "shift maintenance supervisor for section Y"), not to a specific physical terminal or person. When staff log into a GSM-R terminal, they enter their functional number for the duty they're performing, and the network routes calls addressed to that function to whichever physical terminal is currently logged in with it — the network resolves the functional number to the terminal dynamically, using the HLR/VLR infrastructure (see network-architecture fundamentals file) extended with this role-mapping capability. This is why, for example, a signaller can call "the driver of train 1234" without knowing which physical cab radio or which individual driver is on duty — the call is addressed to the role, not the person or device.

## Call types

- **Point-to-point call** — one-to-one, addressed either to a functional number or (less commonly in operational use) directly to a terminal/subscriber identity.
- **VGCS (Voice Group Call Service)** — one-to-many group call, standard 3GPP feature: a group of users (e.g. all staff working a section) join a shared call; any member can transmit (unlike a broadcast call), others listen — the GSM-R application of VGCS typically maps group membership to operational roles/sections rather than a fixed subscriber list, coordinated via the Group Call Register (see network-architecture fundamentals file).
- **VBS (Voice Broadcast Service)** — one-to-many broadcast, receive-only for the group except the originator — used for announcements to a group rather than open discussion.
- **Railway emergency call** — a specially prioritised call type (triggered via a dedicated function, e.g. an emergency call button in the cab) that gets top eMLPP priority and pre-empts other traffic if needed — see the eMLPP fundamentals file.

## Why group calls need multi-cell coordination

A VGCS/VBS group call along a rail corridor often needs to remain active as members move between cells (e.g. a group call involving a moving train and trackside staff spread across several cells) — this is handled by the Group Call Register coordinating the call across every cell it's active in, and is part of why GSM-R needs its own core rather than relying on public-GSM infrastructure that treats group calls as a rarely-used feature rather than a core operational capability.

## Why this matters for design decisions

- Functional addressing should be scoped explicitly as a design requirement early — it drives HLR/VLR sizing (how many functional numbers, how the role-to-terminal login/logout process works operationally) and isn't simply "the same as normal mobile numbering with a different name."
- Group call membership design (which roles/sections belong to which group) is an operational-concept decision the client's operations function should define, similar in spirit to TETRA's talkgroup/fleet-mapping design, but tied to railway operational roles rather than a fixed organisational chart.
- Multi-cell group-call continuity should be explicitly verified during testing (see testing/commissioning fundamentals file) for group calls spanning a train's likely movement range, not just tested within a single cell.

Formal reference: 3GPP GSM specifications (VGCS/VBS as standard features); EIRENE FRS/SRS (functional addressing, and the specific mapping of group-call usage to railway operational roles).
