# Trunking & Erlang Capacity Theory

The method behind capacity dimensioning in the Stage 2 technical specification sequence — read this when the question is "how do I actually calculate how many traffic channels a cell needs."

## Why trunking applies to GSM-R too

Like any cellular/trunked system, a GSM-R cell shares a pool of traffic channels across all the calls it needs to carry at once — drivers, signallers, maintenance teams, group calls — rather than dedicating a channel per user. Erlang theory sizes that shared pool against a target blocking probability, exactly as in general cellular capacity planning.

## The Erlang unit and Erlang-B

One **Erlang** = one channel occupied continuously for the busy-hour measurement period. Traffic intensity:
```
A = (call attempts per busy hour) x (average call holding time in hours)
```
**Erlang-B** (blocked calls lost, not queued) is the standard model for GSM-R voice capacity — a driver or signaller needing a channel expects an immediate connection or an immediate failure indication, not a queued wait, and safety-relevant traffic in particular cannot tolerate queuing delay.

**Worked example:** a cell's busy-hour traffic — driver calls, signaller calls, group calls, maintenance calls — sums to 3.0 Erlangs offered. Target blocking probability 0.5% (0.005, a tighter target than a typical public-GSM 1-2%, reflecting GSM-R's safety-relevant traffic mix). Reading an Erlang-B table (or the recursive formula, see the TETRA fundamentals file's equivalent worked derivation for the method) for A=3.0, B=0.005 gives approximately **N = 10 traffic channels** needed. Fewer channels risks blocking a safety-relevant call attempt during a busy period; more channels than needed wastes scarce R-GSM 900 spectrum.

## Converting channels to carriers

Each 200 kHz GSM carrier provides 8 timeslots (see air-interface fundamentals file), of which at least one is typically reserved for control signalling on the cell's primary carrier (BCCH). So `N` traffic channels from the Erlang-B result translates to `ceil((N + control-channel-overhead) / 8)` carriers — not `N / 8` directly — and every additional carrier consumes more of the limited R-GSM 900 band allocation, which is a genuinely scarce resource compared to a public operator's much larger spectrum holding.

## Why traffic modelling looks different from a public network

- **Group calls (VGCS/VBS)** consume traffic channel resources differently from point-to-point calls — a group call spanning multiple cells occupies a channel in every cell it's active in simultaneously, which needs to be accounted for separately from ordinary point-to-point Erlang traffic, not folded into the same traffic-intensity figure without adjustment.
- **Safety-relevant call priority (eMLPP)** means the "blocking probability" target itself may need to be tiered — an emergency call effectively cannot be blocked (it pre-empts, per the eMLPP fundamentals file), so the Erlang-B blocking target really applies to the non-pre-emptible portion of traffic, with pre-emption as the mechanism protecting the highest-priority calls beyond what raw capacity alone guarantees.
- **Busy-hour profile is operationally driven**, not a generic assumption — a station/yard cell's busy hour looks different from an open-track cell's, and both differ from a depot's; always source actual or projected call-attempt data per cell type rather than applying one blanket traffic model network-wide.

## Why this matters for design decisions

- This is the actual calculation method behind whatever traffic-dimensioning item exists in the Stage 2/3 sequences (worth confirming exactly where Harish's correction places it, since it's currently implicit rather than a named checklist item in this skill's draft).
- R-GSM 900's limited bandwidth makes over-provisioning carriers a real cost/feasibility issue, unlike a public operator with far more spectrum — capacity planning accuracy matters more here.
- Group-call traffic and eMLPP pre-emption both change how the raw Erlang-B model should be applied compared to a textbook single-traffic-class calculation — flag this as a design nuance, not something to gloss over.

Formal reference: general telecom traffic engineering (Erlang, 1917) applied to GSM/GSM-R capacity planning; EIRENE FRS/SRS for the railway-specific traffic classes (group calls, eMLPP tiers) layered on top.
