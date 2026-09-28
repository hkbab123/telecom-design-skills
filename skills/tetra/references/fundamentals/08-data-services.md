# Data Services (SDS & Packet Data)

What "provision for data" in Stage 2 item 6/9 technically means.

## Short Data Service (SDS)

TETRA's equivalent of a text/status message, carried over the control channel (not a dedicated traffic channel), so it doesn't consume the same trunked capacity as voice. Two main forms:
- **Status messages** — a predefined short code (e.g. "en route," "on scene," "task complete") mapped to operational meanings by the client — very low bandwidth, near-instant.
- **Free-text SDS** — short free-form text messages, still control-channel-carried but with a length limit far below a modern SMS.

Common uses: GPS location reporting (a terminal periodically sends its position as an SDS payload — this is how fleet-tracking/GPS features mentioned in Stage 2 item 12 are actually implemented technically), lone-worker check-in status, dispatcher-to-field short instructions.

## Packet data

For larger data payloads (beyond SDS's scope), TETRA supports **packet data service** carried over a traffic channel (unlike SDS, this does consume trunked capacity and needs its own Erlang-style dimensioning if the volume is significant). Throughput is modest compared to any broadband technology (well below what LTE/5G would offer) — TETRA packet data is suited to telemetry, SCADA polling, or other low-bandwidth machine-to-machine traffic, not file transfer or video. This ceiling is the core technical reason a broadband/MCPTT migration path (see the migration fundamentals file) becomes relevant once a client's data needs grow beyond simple telemetry.

## Why this matters for design decisions

- If GPS/fleet tracking is required (Stage 2 item 12), the actual data path is SDS — dimension for periodic SDS traffic on the control channel, don't assume it needs dedicated traffic-channel capacity unless reporting frequency is unusually high.
- If SCADA/telemetry integration is in scope (Stage 2 item 13's O&M/asset systems interface), check whether the data volume fits TETRA packet data's modest throughput ceiling or actually needs a separate data-bearer (a private LTE network, wired SCADA link, etc.) — don't assume TETRA can carry high-volume telemetry.
- Any client request that sounds like "send photos/video over the radio network" is out of scope for TETRA's data services entirely — flag it as a broadband/MCPTT migration conversation, not a TETRA data-service configuration question.

Formal reference: ETSI EN 300 392-2 (SDS), ETSI EN 300 392-3 / 392-8 series (packet data).
