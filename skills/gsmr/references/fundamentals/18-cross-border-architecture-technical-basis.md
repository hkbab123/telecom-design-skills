# Cross-Border Architecture — Technical Basis

A deeper technical companion to `SKILL.md`'s Step 2 core-placement decision and the network-architecture fundamentals file (02) — read this when the question is "what actually makes the independent-core-plus-interworking architecture work, mechanically."

## The interworking interface, mechanically

When a train crosses the border, three things need to keep working without interruption or manual intervention:
1. **Voice/data call continuity** — a call in progress (point-to-point or group) needs to hand over from one country's core to the other's, analogous in principle to an inter-cell handover (fundamentals file 05) but happening at the inter-core/inter-network level rather than within a single core's BSC.
2. **Functional-number resolution across cores** — a functional number registered/logged-in under one country's HLR needs to remain reachable (and the driver's login session needs to persist) as the train's serving core changes — this requires the two cores' HLR/VLR infrastructure to exchange location/registration information via the interworking interface, not just route voice traffic.
3. **Group call continuity across the border** — a VGCS/VBS group call spanning the border (e.g. a cross-border operational group) needs Group Call Register coordination across both cores, an even more demanding requirement than simple call handover, since it involves coordinating group membership state across two independently-operated systems.

## Why "shared/stretched core" avoids some of this complexity, but at an architectural cost

A single shared core spanning both countries would avoid needing an inter-core interworking interface at all (everything happens within one core's own internal mechanisms) — which is precisely its appeal and why some past projects have used it. But this convenience comes at the cost flagged in the network-architecture fundamentals file: regulatory/licensing ambiguity (whose national regulator governs a core physically/logically spanning two jurisdictions), single point of failure spanning both countries' operations, and ambiguous operational/maintenance ownership. The independent-core-with-interworking architecture deliberately takes on the interworking-interface engineering complexity described above in exchange for avoiding these structural weaknesses.

## Regulatory and operational alignment

Beyond the pure network-engineering question, the independent-core architecture keeps each country's railway administration in full operational and regulatory control of its own domestic infrastructure — spectrum licensing (frequency-planning fundamentals file's cross-border coordination point), maintenance responsibility, incident response, and safety-case ownership all remain cleanly within national boundaries, with only the interworking interface itself being a genuinely bilateral/shared concern requiring joint agreement between the two administrations.

## Why this matters for design decisions

- The interworking interface (call continuity, HLR/VLR coordination, group-call coordination) should appear as an explicit, detailed deliverable in a cross-border project's technical specification and detailed design — not treated as a solved problem simply because "both sides use GSM-R."
- This is a genuinely bilateral engineering exercise requiring agreement and coordination between two potentially different vendors/integrators and two national railway administrations — project planning should account for this coordination overhead explicitly, distinct from either country's own domestic design work.
- This file, along with the network-architecture fundamentals file, is the direct technical justification behind the architecture correction Harish provided from the real Hafeet Rail cross-border reference (see `GSMR Skill.md`'s Reference Case Study) — worth citing together when explaining the recommendation to a client or reviewer unfamiliar with why it matters.

Formal reference: EIRENE FRS/SRS (cross-border interoperability requirements); 3GPP GSM interworking mechanisms (the underlying inter-network signalling capability the interworking interface builds on).
