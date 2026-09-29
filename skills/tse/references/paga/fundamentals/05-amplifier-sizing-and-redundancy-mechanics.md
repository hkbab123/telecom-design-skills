# Amplifier Sizing and Redundancy Mechanics

Underpins Stage 2 item 5 (redundancy and availability) — read this for how amplifier redundancy actually works mechanically, not just "specify N+1."

## Why amplifier redundancy matters more here than in a typical audio system

In a background-music PA system, an amplifier failure is an inconvenience. In a PAGA system carrying the General Alarm function, an amplifier failure during an actual emergency means a zone of people don't receive the evacuation instruction that's meant to save their lives — this is precisely why GA-carrying amplifier circuits are held to a materially higher redundancy standard than PA-only equipment (fundamentals file 01's PA/GA split matters here directly).

## N+1 vs dual-redundant (2N)

- **N+1 redundancy** — one spare amplifier covers any single failure across a group of N amplifiers, with an automatic switchover mechanism detecting the failed unit and routing its load to the spare. Economical (one spare covers many active units) but only protects against a single simultaneous failure, and the switchover process itself takes a finite time (confirm the actual failover time with the OEM — it is not instantaneous by default).
- **Dual-redundant (2N)** — every amplifier circuit has a fully duplicated, independently powered standby amplifier running (or ready to run) in parallel, giving near-instant failover with no shared spare-capacity constraint. More expensive (doubles amplifier hardware) but the standard expectation for the most safety-critical GA circuits on a facility where an emergency-response safety case actually depends on it.

The choice between the two — and whether it's applied uniformly or varies by zone criticality — is a design decision to make explicitly against the client's risk tolerance and (where SIL-rated, fundamentals file 07) the functional-safety requirement, not defaulted to whichever is cheaper.

## What actually triggers failover

An amplifier failure needs to be **detected** before it can be switched over — this is a distinct mechanism from loudspeaker-line supervision (fundamentals file 06), which detects cable faults downstream of a working amplifier. Amplifier-level fault detection typically monitors the amplifier's own health (output stage fault, overheat, power-supply failure) and, on detecting a fault, either automatically switches the affected line(s) to a standby amplifier (N+1) or confirms the parallel standby unit (2N) is already carrying the load. The switchover mechanism itself, and its actual failover time, is an OEM-specific implementation detail to confirm rather than assume — "redundant" without a stated failover-time figure is an incomplete specification.

## Power supply and controller redundancy — don't stop at the amplifier

Amplifier redundancy alone doesn't close every single point of failure: the **central controller/matrix** (fundamentals file 01) that routes calls to zones, and its **power supply**, can each independently take down GA capability even with fully redundant amplifiers behind them. A complete redundancy design addresses all three layers — amplifier, controller, and power — rather than treating "amplifier redundancy" as synonymous with "system redundancy."

## Why this matters for design decisions

- Stage 2 item 5's redundancy target should specify N+1 vs 2N explicitly, per zone criticality (GA zones especially) rather than one blanket redundancy statement for the whole system.
- Confirm the actual failover time from the OEM for whichever redundancy scheme is chosen — this is a real design parameter, not an assumed-instant capability, and matters directly to the reliability/safety case (Stage 2 item 15).
- Redundancy design must address the central controller and power supply layers, not stop at the amplifier — a fully redundant amplifier bank behind a single non-redundant controller still has a single point of failure for the whole system.

Formal reference: no single standard mandates a specific redundancy architecture; EN 54-16 sets minimum equipment reliability/fault-indication requirements the redundancy design must ultimately support, and IEC 61508/61511 apply where the GA function is formally SIL-rated (fundamentals file 07).
