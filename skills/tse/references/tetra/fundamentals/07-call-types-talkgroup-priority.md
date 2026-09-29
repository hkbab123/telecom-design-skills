# Call Types, Talkgroup Mechanics & Priority/Pre-emption

The technical mechanics behind Stage 2 items 6 and 12 — read this when the question is "how does a group call actually work" or "what does pre-emption mean technically."

## Call types

- **Group call** — one-to-many, the core PMR use case. A talkgroup member presses PTT (push-to-talk); the SwMI grants a traffic channel and connects every other member currently listening to that talkgroup (across however many cells they're distributed on — the SwMI, not the base station alone, coordinates this). Half-duplex: one speaker at a time, others listen.
- **Individual call** — one-to-one, can be full-duplex (like a phone call) or half-duplex depending on terminal/network configuration. Used for private conversations outside the group context.
- **Broadcast call** — one-to-many, receive-only for the group (no one can transmit back on that call) — used for announcements.
- **Emergency call** — a specially flagged call type (usually triggered by a dedicated emergency button on the terminal) that gets top priority handling — see pre-emption below.

## Talkgroup addressing and scanning

A talkgroup is a logical address, not a physical channel — the SwMI dynamically allocates a traffic channel to a group call only for its duration, freeing it immediately after (this is the trunking principle from the Erlang fundamentals file in action). A terminal can be a member of multiple talkgroups and **scan** across them (monitoring several groups, automatically following whichever one has active traffic) — the scan list is part of the terminal's provisioning (see the terminal/codeplug fundamentals file).

## Dynamic Group Number Assignment (DGNA)

Normally a terminal's talkgroup memberships are fixed by its provisioned codeplug. **DGNA** lets the network dynamically add or remove a talkgroup from a terminal's active list over the air — used for incident response (temporarily pulling specific field units into an emergency-coordination talkgroup without re-programming radios) or flexible task-based regrouping. If a client's operational concept includes forming ad-hoc groups on demand, DGNA needs to be an explicit requirement — it isn't automatic.

## Priority and pre-emption

Every call in TETRA can be assigned a **priority level**. When channel resources are scarce (all traffic channels busy), a higher-priority call attempt can **pre-empt** (forcibly terminate) a lower-priority call in progress to free a channel. This is directly analogous to eMLPP (used in GSM-R) but implemented within the TETRA standard's own priority mechanism rather than borrowed from cellular. Emergency calls are typically configured at the highest priority tier, ensuring they always get a channel even under network congestion — this is a design requirement to confirm explicitly with the client (how many priority tiers, which call types map to which tier), not a technical default.

## Why this matters for design decisions

- Priority/pre-emption policy (Stage 2 item 12) has real technical teeth — it isn't just a console feature, it changes which calls survive under congestion, which is safety-relevant for O&G emergency response.
- DGNA is easy to miss as a requirement if the client describes their operational concept only in terms of "normal" fixed talkgroups — worth asking about explicitly during Stage 2 item 6.
- Scan-list design (which groups a given radio monitors) is a provisioning decision with real operational consequences (missing a group's traffic vs radio congestion from monitoring too many) — flagged in the terminal/codeplug fundamentals file.

Formal reference: ETSI EN 300 392-2 (call control, group management, priority mechanisms).
