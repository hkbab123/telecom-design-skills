# Cybersecurity & IT/OT Segmentation

The method behind Stage 2 item 6 and Stage 3 item 8 — read this when the question is "how does IEC 62443 segmentation actually work," not just "decide the segmentation requirement." This is the technical basis for Subsystem-specific rule 3.

## Why OT security is a different discipline from IT security

IT security prioritises confidentiality first, generally tolerates brief downtime for patching, and assumes endpoints can be rebooted/updated frequently. OT security inverts these priorities: **availability and integrity come first** (a SCADA server going down mid-shift, or a control command being corrupted, is far more consequential than a confidentiality breach of, say, historian trend data), patching is often deferred or tightly scheduled around planned outages (a live plant/tunnel-ventilation system can't simply be rebooted whenever a patch releases), and many field devices (RTUs, PLCs) have limited or no capacity to run endpoint security software at all. A corporate IT security policy copied unchanged onto an OT network usually gets both the priorities and the practicalities wrong.

## Zones and conduits (IEC 62443)

- **Zone** — a grouping of assets that share the same security requirements (e.g. "the SCADA supervisory network," "the RTU/PLC control network," "the corporate IT network") — each zone gets a security level target.
- **Conduit** — the pathway (physical or logical) connecting zones, where security controls (firewalls, one-way data diodes, jump servers) are actually implemented — the model's core insight is that security is enforced at the conduit, not scattered per-device inside each zone.

## Typical architecture: three zones with a DMZ

A common pattern: **OT zone** (SCADA servers, RTU/PLC network) — **DMZ** (a buffered middle zone holding, e.g., a historian mirror or a data-exchange server, so nothing in the OT zone talks directly to the IT zone) — **IT/corporate zone**. The DMZ is the conduit-enforcement point: IT-zone systems pull data from the DMZ mirror, never reach directly into the OT zone; and OT-zone systems push only the specific data needed to the DMZ, never accept inbound connections from IT.

## Remote access

If remote access into the OT zone is required (vendor support, remote engineering), it should go through a controlled, time-limited, logged jump-server/VPN mechanism sitting in the DMZ — never a direct, always-on connection from the corporate network or the internet into the OT zone.

## Why this matters for design decisions

- Stage 2 item 6 exists as an explicit, early specification item precisely because retrofitting segmentation after a network is built (and contractors have wired whatever was fastest) is expensive and disruptive — specify the zone/conduit model before equipment procurement, not after.
- This is the technical reasoning behind Subsystem-specific rule 3 — "IT/OT segmentation is a design requirement from day one."

Formal reference: IEC 62443 series (particularly 62443-3-2 for zone/conduit risk assessment, 62443-3-3 for system security requirements by security level).
