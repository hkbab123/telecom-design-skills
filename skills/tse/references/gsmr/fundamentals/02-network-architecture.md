# Network Architecture

The physical/logical system behind "the network" and "the core" referenced throughout Stage 2/3, and the technical basis for the cross-border core-placement decision.

## Standard GSM core elements, as used by GSM-R

- **BTS (Base Transceiver Station)** — the trackside radio site; each covers a section of line (a cell).
- **BSC (Base Station Controller)** — controls a group of BTSs: handover decisions, radio resource management, power control.
- **MSC (Mobile Switching Centre)** — the core switching function: call routing, mobility management, interworking with other networks. GSM-R networks typically run their own dedicated MSC(s), separate from any public operator's core, precisely because of the railway-specific features (eMLPP, VGCS/VBS, functional addressing) that a shared public core wouldn't support.
- **HLR/VLR (Home/Visitor Location Register)** — subscriber/terminal location and service-profile database, standard GSM mobility infrastructure, additionally carrying the functional-number-to-terminal mapping GSM-R needs (see the functional-numbering fundamentals file).
- **Group Call Register (GCR)** — a GSM-R/EIRENE-specific network element managing active VGCS/VBS group calls across the cells they span — this has no direct public-GSM equivalent at the same operational importance, since group calls are a niche public-GSM feature but core to GSM-R operations.

## Why GSM-R needs its own core, even domestically

A public mobile operator's core network has no reason to implement eMLPP priority for a train driver's emergency call, VGCS for a signaller's group call to a maintenance team, or functional addressing tied to a specific duty/role rather than a SIM card. This is the fundamental reason GSM-R networks are built and operated independently of public mobile infrastructure, even though they share the underlying GSM standard — not a spectrum/interference argument alone (covered in the air-interface file), but a functional-capability argument.

## Cross-border core placement — the technical mechanics behind the recommended architecture

As established in `SKILL.md`'s Step 2, the recommended default for cross-border lines is **an independent core per country, with interworking**, rather than one shared core split only across control centres. The technical reasoning:

- **Independent core per country + interworking** — each country's railway administration operates its own MSC/BSC/HLR infrastructure, with a defined interworking interface (routing calls and, critically, maintaining seamless group calls and functional-number resolution) to the neighbouring country's core when a train crosses the border. This keeps each country's core under its own national railway administration's operational and regulatory control (spectrum licensing, maintenance responsibility, incident response) while still providing continuity of service across the border — the interworking interface is the technical mechanism that makes "independent but interoperable" actually work, not just a policy statement.
- **Shared/stretched core, split only across primary/backup control centres** — architecturally weaker specifically because it makes the core network itself a cross-border shared asset: regulatory/spectrum licensing complications (whose national regulator governs a shared core?), a single core failure affects both countries' rail operations rather than being contained to one, and operational/maintenance responsibility becomes ambiguous. This is why the independent-core recommendation exists — not an arbitrary preference, but a direct consequence of keeping national regulatory/operational boundaries aligned with network boundaries.

## Why this matters for design decisions

- Every EIRENE-specific feature (eMLPP, VGCS/VBS, functional addressing) ultimately depends on GSM-R's dedicated core elements (MSC, GCR, enhanced HLR) — this is why "can we just extend the public operator's core" is never a viable answer, worth having ready as an explanation if a client or reviewer asks.
- The cross-border interworking interface (between two independent national cores) is itself a real engineering deliverable in Stage 2/3 for cross-border projects — it should appear explicitly in the interfaces checklist, not be assumed to happen automatically because "both cores are GSM-R."

Formal reference: 3GPP GSM core network specifications (MSC/BSC/HLR baseline); EIRENE FRS/SRS (GCR, functional addressing, and the cross-border interworking requirement).
