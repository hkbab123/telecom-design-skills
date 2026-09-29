# Redundancy & Availability Mechanics

The method behind Stage 2 item 7 and Stage 3 item 9 — read this when the question is "how does SCADA redundancy actually fail over," not just "decide the redundancy level."

## SCADA server redundancy

The most common pattern is a **hot-standby pair**: two SCADA servers continuously synchronised (same tag database, same historian data mirrored), one active, one standby. On active-server failure (or a manually triggered switch for maintenance), the standby takes over — the key design parameters are the failover time (how long operators lose visibility, ideally seconds not minutes) and the synchronisation mechanism (how current the standby's data is at the moment of failover — a lagging sync means data loss on failover, not just a visibility gap).

## RTU/PLC redundancy

Justified selectively, not everywhere — a redundant PLC pair (dual processors, bumpless failover) is common where a single controller failure would be operationally serious (a tunnel-ventilation fan-control PLC during an emergency event) but is often not justified for a low-consequence monitoring-only RTU. State the justification per site/function rather than applying one redundancy policy uniformly.

## Network redundancy

- **Ring topology** (e.g. a fibre ring with a fast ring-protection protocol) — a single cable break doesn't isolate any site, traffic reroutes around the ring.
- **Dual-homed** — each RTU/PLC panel has two independent network paths to the SCADA server, typically over separate physical routes, so a single point of cable damage doesn't isolate that site.

Both aim at the same design principle: no single point of failure between a field site and the point an operator can see its data.

## Availability as a target, not a design in itself

An "availability target" (e.g. 99.9%) is the outcome the redundancy design above should be able to demonstrate, not a separate thing to specify independently of it. Confirm the target's basis explicitly: is it measuring SCADA-server availability, network-path availability to a given site, or end-to-end (field device to operator screen)? These are different numbers, and a bidder can honestly meet one while failing another if the specification doesn't say which is meant.

## Why this matters for design decisions

- Stage 2 item 7's "state the target explicitly per use case" instruction exists because a rail tunnel-ventilation emergency-mode availability requirement and a station pump-status convenience-monitoring requirement genuinely warrant different redundancy investment — don't apply one blanket target to both.
- Redundancy that isn't tested (see the testing/commissioning fundamentals file) is a specification, not a proven capability — Stage 3's FAT/SAT plan should include an actual failover test, not just a design review.

Formal reference: general industrial-control redundancy practice; no single governing standard, but referenced implicitly wherever IEC 61508/61511 discuss architecture redundancy for safety-related functions.
