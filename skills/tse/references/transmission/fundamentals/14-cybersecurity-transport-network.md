# Cybersecurity of the Transport Network

**Why this matters:** the transport network connects every operational subsystem; compromising it can compromise all of them. It also carries traffic across zones, so segmentation depends on it.

## Management plane

- Separate management traffic (DCN) from user traffic; never expose management interfaces on service VLANs.
- Strong authentication (centralised AAA, e.g. RADIUS/TACACS+), role-based access, session logging.
- Disable unused services and default accounts; baseline hardening per vendor guide and IEC 62443 principles.
- Secure protocols only (SSH, HTTPS, SNMPv3); retire Telnet, HTTP and SNMPv1/v2c where possible.

## IT/OT segmentation

Transport nodes carry traffic from both operational (SCADA, signalling-adjacent, PAGA) and enterprise domains. Keep them in separate services (VLAN/VPN/wavelength) with no uncontrolled path between them; enforce boundaries at firewalls/zone conduits, following IEC 62443 zones-and-conduits thinking (see SCADA `fundamentals/06-cybersecurity-it-ot-segmentation.md`).

## Encryption options

- **MACsec (IEEE 802.1AE)** on links; **OTN-layer encryption** or **IPsec** for services crossing untrusted segments, e.g. leased fibre.
- Weigh performance, latency, key management and operational complexity.

## Physical security

Fibre is tappable at joints and access points. For leased or shared routes consider encryption; for owned routes control joint-closure access, alarm node-room doors, and monitor optical power for tamper signs.

## Supply-chain and vendor compliance

Same rule as CCTV: many projects exclude specific equipment manufacturers by name on national-security grounds. Confirm the requirement at Tender stage, before building any OEM shortlist, and verify it again on the actual delivered components and firmware.

## Patching and lifecycle

Plan firmware updates with maintenance windows and rollback; record the baseline in as-built documents.

## Common mistakes

- Management VLAN reachable from the enterprise network.
- Shared admin credentials across nodes.
- Treating owned fibre as inherently secure.
