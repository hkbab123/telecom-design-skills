# Air Interface & Protocol Architecture

What TETRA actually does at the radio/protocol level — read this when a question is "how does TETRA work" rather than "what do I decide next."

## TDMA structure

TETRA uses TDMA (Time Division Multiple Access) with **4 timeslots per RF carrier**, each carrier occupying a **25 kHz** channel (narrower variants exist but 25 kHz is the baseline in EN 300 392). One physical carrier therefore supports up to 4 simultaneous logical channels — this is why a single TETRA base station carrier can carry roughly 4x the voice traffic of an equivalent analogue FM channel, and it's the reason TETRA capacity planning counts **timeslots**, not carriers, as the basic capacity unit (see the trunking/Erlang fundamentals file).

Frame structure, top-down:
- **Multiframe** — 18 TDMA frames, the 18th reserved for control signalling (frame 18 carries the control channel in idle/control mode).
- **Frame** — 4 timeslots (one per user, on a single carrier).
- **Timeslot** — the basic transmission unit; a burst of modulated symbols ~14.167 ms long.

## Modulation

**π/4-DQPSK** (differential quadrature phase-shift keying, π/4 rotation) — a spectrally efficient digital modulation carrying 2 bits per symbol. Chosen for a good balance between spectral efficiency (fits 4 users in 25 kHz) and robustness against multipath in the kind of environments TETRA is deployed in (urban, tunnels, industrial plant — all multipath-heavy). This is a fixed design choice of the standard, not something the engineer selects.

## Logical channels

Two broad categories, both mapped onto the TDMA timeslot structure:
- **Traffic channels (TCH)** — carry the actual voice or user data.
- **Control channels** — carry signalling: call setup, registration, group attachment. The **Main Control Channel (MCCH)** handles this in idle mode; the **Signalling Channel (SCH)** carries signalling during an active call (e.g. mid-call priority changes).

## TMO vs DMO at the protocol level

- **TMO (Trunked Mode Operation)** — the terminal communicates via the SwMI (base station → exchange → destination). This is what "the network" means in every Stage 2/3 decision in this skill.
- **DMO (Direct Mode Operation)** — terminals communicate directly with each other on a shared DMO channel, entirely bypassing the SwMI. Protocol-wise this is a much simpler point-to-multipoint scheme: one terminal (or a role called "DMO master" in some deployments) controls channel access, others listen/transmit on it. No handover, no trunking, no call setup via an exchange — this is why DMO coverage is limited to direct radio range and why DMO calls can't easily interoperate with TMO users without a gateway (see the DMO fundamentals file).

## Why this matters for design decisions

- Timeslot-based capacity (not carrier-based) is why the Erlang-B capacity calculation in Stage 2 item 7 works the way it does.
- The MCCH/SCH split is why "control channel capacity" is sometimes a separate dimensioning check from voice traffic channel capacity on busy sites.
- The TMO/DMO protocol split is why item 10 (DMO requirement) is a binary design decision with real architectural consequences, not a minor feature toggle.

Formal reference: ETSI EN 300 392-2 (air interface). Figures above (25 kHz, 4 timeslots, 18-frame multiframe) are the EN 300 392 baseline — confirm against the specific standard revision if a project cites an unusual band plan or narrowband variant.
