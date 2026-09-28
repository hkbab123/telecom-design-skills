# Interfacing Technical Basis (Beyond F&G/ESD)

Underpins Stage 2 item 13 (interface family, the general case) — read this alongside fundamentals file 09, which covers the F&G/ESD interface specifically; this file covers the other interfaces PAGA commonly needs, and the general principles for scoping any interface correctly.

## The general interfacing principle: who owns which side

Every PAGA interface connects to a system owned and specified by someone else — a fire panel, a telephony system, a building management system, a train describer. The recurring discipline across all of them is the same: **PAGA implements its side of the interface against the other system's documented interface specification, not against an assumption of how that system probably behaves.** An Interface Control Document (ICD), jointly agreed and signed off by both sides, is the correct mechanism for capturing this — informal verbal agreement on interface behaviour is a common source of late-stage integration failures precisely because each side quietly assumed something slightly different.

## Common PAGA interfaces beyond F&G/ESD

- **Telephony/PABX integration** — allowing a phone extension to trigger a page or announcement, common in both rail station environments (staff paging from an office extension) and O&G control rooms. Typically a lower-criticality interface than F&G/ESD, but still needs its own defined trigger mechanism and access-control logic (who's authorised to page which zones from which extension).
- **Building Management System (BMS) / SCADA integration** — for facilities where broader building or plant automation systems need visibility into PAGA status (is GA currently active, is a fault present) or need to trigger PA announcements based on other automated conditions. Confirm the specific data points and trigger conditions needed, rather than assuming a generic "connect the two systems" scope.
- **CCTV/access control correlation** — some designs link PAGA zone activation to CCTV camera calls (automatically bringing up the relevant camera view when a zone alarms) — a genuinely useful operational feature, but an optional enhancement to scope explicitly if wanted, not an assumed baseline requirement.
- **Rail-specific: train describer / passenger information system integration** — on rail platforms, automated next-train or delay announcements are commonly triggered from the train describer or passenger information system rather than manually by station staff — see fundamentals file 18 for the rail-specific detail on this interface.

## Interface criticality tiering

Not every interface needs the same rigor as F&G/ESD. A useful discipline is explicitly tiering each interface by what happens if it fails: an F&G/ESD interface failure could delay a life-safety response (highest criticality, warranting the full ICD/cause-and-effect-matrix rigor of fundamentals file 09); a telephony-paging interface failure is an inconvenience (lower criticality, a simpler interface spec is proportionate). Stating this tiering explicitly in Stage 2 item 13 helps avoid both under-engineering the safety-critical interface and over-engineering the low-criticality ones.

## Why this matters for design decisions

- Stage 2 item 13 should list every interface the project actually needs — not just F&G/ESD — with an owner, a criticality tier, and confirmation that an ICD (or equivalent joint specification) exists or will be produced for each.
- Lower-criticality interfaces (telephony, BMS) still need a defined trigger mechanism and access-control logic — don't leave these implicit just because they're not life-safety-critical.
- Rail projects should explicitly check whether train describer/PIS integration is in scope early, since it affects the message-content and trigger-logic design differently from a purely manually-operated station PA system.

Formal reference: no single standard governs general system-to-system interfacing for PAGA; each interface is scoped against the connected system's own documented interface specification, with EN 54-16/IEC 60849 setting the baseline PAGA-side performance requirement regardless of which external system triggers it.
