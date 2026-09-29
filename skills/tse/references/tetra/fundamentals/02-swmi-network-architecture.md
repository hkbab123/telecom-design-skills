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

## Fallback/local-site trunking on backhaul loss

If a base station loses its transmission link back to the exchange (fundamentals file 14), a well-specified site doesn't simply go dead — most TETRA base stations support a **fallback mode** (sometimes called local-site trunking or isolated-site operation) where the base station itself takes over basic trunking functions for terminals still within its own radio coverage: normal group/individual calls between terminals on that one site continue to work, using the base station's own local switching logic, even though it's cut off from the wider network and from other sites' terminals. What's typically **lost** in fallback mode (confirm exact behaviour against the specific OEM's implementation — this varies): calls to/from terminals on other sites, dispatcher console connectivity to that site (since the dispatcher connects via the exchange), OTAR/authentication updates, and often any DMO gateway/repeater functions the site was providing. Fallback capability should be an explicit technical-specification requirement (Stage 2 item 4, alongside the wider redundancy targets — see fundamentals file 15) for any site where backhaul reliability can't be guaranteed to the same standard as the core network, particularly a genuinely isolated remote site (a rural rail halt, a remote pipeline block valve station) rather than a well-connected urban/plant site.

## Why this matters for design decisions

- Fallback/local-site trunking should be scoped explicitly as a requirement for remote or backhaul-vulnerable sites, with the specific OEM's fallback behaviour (what's retained, what's lost) confirmed against its datasheet rather than assumed uniform across vendors.
- Exchange topology (single vs multi) is the real content behind Stage 2 item 3's "SwMI architecture" decision — it isn't just "how many base stations," it's "how many exchanges and how do they relate."
- ISI is the answer when a client asks "can our TETRA network talk to that other TETRA network" — a question that doesn't fit neatly into any single Stage 2 item as currently drafted, worth flagging to Harish as a possible missing checklist item.
- Simulcast vs conventional is a real architecture fork inside Stage 2 item 3/8 (coverage philosophy + link budget) that the current draft doesn't call out explicitly — another candidate correction.

Formal reference: ETSI EN 300 392-3 (interworking, including ISI).
