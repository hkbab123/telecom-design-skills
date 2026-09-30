# Network Design for CCTV

**Dedicated VLAN/subnet.** CCTV traffic is typically segregated onto its own VLAN, separate from general IT/office traffic and (per rule around IT/OT boundaries, same discipline as SCADA) separate from any OT/process-control network. This contains the bandwidth impact of video traffic, simplifies QoS policy, and reduces the CCTV network's exposure to/from other systems.

**Multicast for live viewing.** If five operators all view the same camera's live stream over unicast, the network carries that camera's bitrate five times. Multicast lets the network deliver one stream that multiple viewers subscribe to — essential once a project has more than a handful of concurrent viewing clients, or a large video wall.

**QoS (Quality of Service).** Video traffic is latency- and jitter-sensitive for live viewing (not for recording, which can tolerate more buffering) — prioritise live-view/control traffic over bulk recording-to-storage traffic where they share a network segment.

**PoE (Power over Ethernet) budgeting.** IP cameras are typically PoE-powered — each switch has a total PoE power budget, and camera count × per-camera power draw (higher for PTZ/heated housings than for a basic fixed camera) must stay within it, with margin. This is a real constraint that gets missed when cameras are added late to a design without rechecking switch capacity.

**Why this matters for design decisions:** network design decisions here (VLAN segregation, multicast, PoE budget) directly gate Stage 3 items 6 and 11 (network architecture detailed design, power system design) — get the architecture principle right at Tender stage so Engineering stage is sizing against a settled plan, not re-deciding it.

**Formal reference:** IEEE 802.1Q (VLAN), IEEE 802.3af/at/bt (PoE/PoE+/4PPoE), IETF RFC standards for IGMP (multicast group management).
