# Trunking & Erlang Capacity Theory

The method behind Stage 2 item 7 — read this when the question is "how do I actually calculate how many traffic channels I need," not just "decide the traffic channel count."

## Why trunking exists

A trunked system shares a pool of traffic channels across many talkgroups, rather than dedicating one channel per group. This works because not every talkgroup transmits simultaneously — trunking exploits that statistical sharing to serve far more users per channel than a dedicated-channel scheme, at the cost of occasional call queuing/blocking when many groups want a channel at once. Erlang theory is the mathematics of sizing that shared pool so blocking stays within an acceptable target.

## The Erlang unit

One **Erlang** = one channel occupied continuously for the measurement period (typically the busy hour). Traffic intensity `A` (in Erlangs) for a talkgroup:

```
A = (call attempts per busy hour) x (average call holding time in hours)
```

**Worked example:** a talkgroup has 40 call attempts in the busy hour, average call duration 12 seconds (0.00333 hours):
```
A = 40 x 0.00333 = 0.133 Erlangs
```
Sum `A` across all talkgroups sharing a site's channel pool to get total offered traffic.

## Erlang-B

Used when blocked calls are **lost** (no queuing) — the standard assumption for PMR voice, since a dispatcher/field user expects an immediate channel or an immediate busy signal, not a queued wait. Erlang-B relates three variables: offered traffic `A` (Erlangs), number of channels `N`, and blocking probability `B` (grade of service, e.g. 1% = 0.01, meaning 1 in 100 call attempts is blocked).

The formula (recursive form, easiest to compute):
```
B(N, A) = [A x B(N-1, A)] / [N + A x B(N-1, A)]
B(0, A) = 1
```

**Worked example:** total offered traffic on a site = 2.5 Erlangs, target blocking = 1% (0.01). Iterating the recursion (or reading an Erlang-B table) gives **N = 8 channels** needed to hold blocking at or below 1% for 2.5 Erlangs offered. Fewer channels (say 6) would push blocking above the 1% target; more channels than needed wastes spectrum/hardware.

In practice: use a published Erlang-B table or calculator rather than iterating the recursion by hand on a live project — the formula above is so the engineer understands *what the table is doing*, not to replace it.

## Erlang-C (when it applies)

Assumes blocked calls **queue** rather than being lost. Rarely the right model for TETRA voice (see above) but can apply to non-priority data traffic (e.g. bulk SDS/telemetry) where a short queuing delay is acceptable. Don't default to Erlang-C for voice capacity dimensioning without a specific reason.

## Converting Erlang capacity to timeslots/carriers

Each traffic channel in the Erlang calculation corresponds to one TDMA timeslot (see air-interface fundamentals file). A single 25 kHz carrier provides 4 timeslots — but not all 4 are necessarily traffic channels; one is typically reserved for control signalling on at least one carrier per site. So `N` channels from the Erlang-B result translates to `ceil((N + control-channel-overhead) / 4)` carriers, not `N / 4` directly.

## Why this matters for design decisions

- This is the actual method behind Stage 2 item 7 — the stage file says "do the calculation," this file is what that calculation *is*.
- Traffic intensity depends heavily on operational profile (rail depot at shift-change vs O&G plant during a normal shift vs an emergency scenario) — always ask for busy-hour call-attempt data specific to the deployment, never assume a generic PMR busy-hour profile.
- Getting the grade-of-service target (1%? 2%? 5%?) wrong changes `N` significantly — this is a client requirement to confirm, not a technical default to assume.

Formal reference: general telecom traffic engineering (Erlang, 1917) — not TETRA-specific, but this is how the industry applies it to trunked PMR capacity planning.
