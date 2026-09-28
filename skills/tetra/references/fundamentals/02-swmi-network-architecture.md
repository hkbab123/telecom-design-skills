# SwMI & Network Architecture

The physical/logical system behind "the network" referenced throughout Stage 2/3.

## What SwMI actually is

**SwMI (Switching and Management Infrastructure)** is the collective term for everything that isn't the radio terminal: the exchange(s), base stations, dispatcher subsystem, and management systems. When Stage 2 item 3 says "size and site the SwMI," it means:

- **Exchange / switch** (often called DXT — Digital eXchange for TETRA — a generic term, not a specific vendor's product name; the actual product is always vendor-specific) — the core switching function: call routing, talkgroup management, mobility management (tracking which base station a terminal is currently registered on), interworking with external networks (PABX, SCADA).
- **Base stations** — the RF sites; each covers a geographic cell, connects back to the exchange via the transmission network (fibre, microwave, or leased circuit — see Stage 3 item 11).
- **Dispatcher subsystem** — consoles used by control-room operators for talkgroup patch, priority override, ambience listening, individual calls (see Stage 2 item 12).
- **Network management system (NMS)** — monitors base station/exchange health, alarms, performance statistics; the operational visibility layer, distinct from the call-handling function itself.

## Single-exchange vs multi-exchange topology

- **Single exchange** — all base stations home to one exchange. Simpler, cheaper, but a single point of failure for the whole network unless the exchange itself is internally redundant (dual/hot-standby — Stage 2 item 4).
- **Multi-exchange / distributed** — multiple exchanges, each serving a region, interconnected. Used for large networks (wide-area O&G with multiple dispersed sites, or a large metro rail network) where a single exchange's capacity or geographic reach isn't sufficient, or where regional resilience is required (one exchange's failure doesn't take down the whole network, only its region).

## Inter-System Interface (ISI)

ETSI-defined interface allowing **separate SwMIs — potentially from different vendors — to interoperate**: calls, talkgroups, and mobility can span two independently-operated TETRA networks. Relevant when: two different organisations' TETRA networks need to interoperate (e.g. a rail operator's TETRA network and an adjacent O&G site's TETRA network, or a merger/expansion connecting two previously separate networks). Not the same as DMO gateway interop (which bridges DMO and TMO, not two SwMIs) — see the DMO fundamentals file.

## Simulcast vs conventional multi-site trunking

- **Conventional trunked multi-site** — each base station is a separate cell; a terminal's call is served by whichever cell it's currently registered on; handover occurs when moving between cells (see fundamentals file 12).
- **Simulcast** — multiple base station sites transmit the *same* signal on the *same* frequency, synchronised, so a terminal experiences one large contiguous coverage area rather than discrete cells. Avoids handover interruptions but requires tight timing synchronisation between sites and careful RF planning to avoid destructive overlap. More common in wide-area coverage where handover-free operation matters (e.g. long linear rail corridors) than in a compact multi-site plant.

## Why this matters for design decisions

- Exchange topology (single vs multi) is the real content behind Stage 2 item 3's "SwMI architecture" decision — it isn't just "how many base stations," it's "how many exchanges and how do they relate."
- ISI is the answer when a client asks "can our TETRA network talk to that other TETRA network" — a question that doesn't fit neatly into any single Stage 2 item as currently drafted, worth flagging to Harish as a possible missing checklist item.
- Simulcast vs conventional is a real architecture fork inside Stage 2 item 3/8 (coverage philosophy + link budget) that the current draft doesn't call out explicitly — another candidate correction.

Formal reference: ETSI EN 300 392-3 (interworking, including ISI).
