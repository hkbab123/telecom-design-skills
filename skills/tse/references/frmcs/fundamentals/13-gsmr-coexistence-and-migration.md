# GSM-R Coexistence and Migration

**Technical basis for Rule 3:** coexistence and migration are design inputs, not a later phase.

*This file is self-contained: it defines the boundary with a legacy GSM-R network from the FRMCS side. It does not require any other subsystem folder.*

## Why it matters

No railway switches its whole network and fleet on one day. For years the legacy radio and FRMCS run side by side, with trains carrying one or both. The design of the coexistence period is where much of the risk, cost and operational disruption lies.

## Situations (Q1b)

- **Greenfield** — no legacy; this file mostly does not apply, except for interoperability with neighbouring networks that still run legacy radio.
- **Overlay** — FRMCS added while the legacy network stays in service, possibly for a long period.
- **Migration** — a planned transition on the same line with defined stages and a legacy end date.

## Coexistence topics

1. **Spectrum and RF** — adjacent carriers, filters, co-sited equipment, intermodulation (`05`).
2. **Site sharing** — masts, shelters, power and backhaul used by both systems; capacity and failure-dependency checks.
3. **Services interworking** — group calls and emergency calls between legacy and FRMCS users via an interworking function; mapping of identities and priorities (`03`).
4. **Train-control data** — a train is controlled over either the legacy bearer or FRMCS; define the handover between them, the switching policy, and what the signalling system accepts (`12`).
5. **Dispatcher and control centre** — consoles must handle both user populations (`18`).
6. **Mixed fleet** — legacy-only, dual-mode and FRMCS-only trains running together; which lines or zones accept which.
7. **Cross-border** — a neighbouring network may still be legacy while yours is FRMCS; the border behaviour must be defined (Q1e).
8. **Operations** — training, procedures, fault management for two systems at once.

## Dual-mode on-board

A dual-mode gateway holds both radios and a policy for which to use where (`11`). Key design items: antenna isolation, which system is primary in each zone, behaviour when both are available, and fallback.

## Migration planning

A staged approach (illustrative):

1. Prepare: baseline pinned, spectrum confirmed, interworking designed.
2. Deploy trackside FRMCS in parallel on a first section; test with equipped trains.
3. Equip the fleet; run dual-mode in service with legacy still the primary.
4. Switch the primary to FRMCS section by section after proven KPI performance.
5. Retain the legacy fallback for a defined period; then decommission.

Each step needs a go/no-go criterion, a rollback path, and a statement of what the signalling approvals allow.

## Decision for the client (surface at Concept)

The client's own timeline for legacy end-of-life is a strategic decision. Do not assume a date or whether the legacy network is a bridge or a full-lifecycle asset; ask.

## Common mistakes

- Treating the legacy network as out of scope in the FRMCS design.
- Dual-mode antennas without an isolation check.
- No rollback plan for cutover.
- Fleet retrofit plan not tied to the trackside programme.
