# Oscillators and Holdover

**Technical basis for Rule 3:** when GNSS goes away, the oscillator decides how long the time stays good.

## Why it matters

A master clock disciplines a local oscillator to the reference. When the reference is lost, the oscillator runs free (**holdover**) and the time error grows. The oscillator class sets how long the master can stay inside the accuracy budget, so it is a design decision, not a datasheet footnote.

## Oscillator classes (illustrative orders of magnitude; confirm with OEM)

| Class | Typical stability character | Typical use |
|---|---|---|
| Crystal (XO) / TCXO | ~1e-6 to 1e-7; drifts noticeably in hours | Cheap embedded clocks, display-clock internal timekeeping |
| OCXO | ~1e-8 to 1e-9 | Standard industrial master clocks |
| Rubidium | ~1e-10 to 1e-11 | Longer holdover, critical masters |
| Caesium | ~1e-12 | Enhanced primary reference time clocks (ePRTC-class) |

Actual holdover depends on temperature stability, ageing, how long the oscillator was disciplined before loss, and drift compensation. These are the reasons holdover is specified as a tested outcome, not just a class.

## The arithmetic

Time error ≈ fractional frequency offset × elapsed time (first-order, constant offset).

**Worked example 1 — constant 1 ppb offset (1e-9):**
1e-9 × 86,400 s = 86.4 µs per day.

**Worked example 2 — how long can an OCXO hold a 1 ms budget at 1e-8?**
1e-8 × t = 1e-3 s → t = 1e5 s ≈ 27.8 hours.

**Worked example 3 — tight consumer, 1 µs budget at 1e-9:**
1e-9 × t = 1e-6 s → t = 1,000 s ≈ 16.7 minutes.

Real oscillators add a drift term that makes the error grow faster than linearly, so these are optimistic first-pass numbers. The same arithmetic shows why a display-clock requirement of seconds is easy over holdover and a microsecond requirement is not.

## Specifying holdover

State it as a tested requirement: "after N hours of disciplined operation with all references present, the master shall remain within X µs/ms of UTC for Y hours after loss of all references". Pick Y from the longest credible outage (antenna fault repair time, interference event, planned maintenance), not from the oscillator's brochure.

## Practical points

- **Warm-up** — a cold OCXO or rubidium oscillator needs time to stabilise after power-on; holdover figures assume it was already stabilised. Power loss longer than the UPS autonomy resets this (see `13`).
- **Recovery** — on return of the reference, the master should slew back to UTC rather than step (see `08`).
- **Sub-masters and display clocks** — a consumer that lost its master is also in holdover on its own cheap oscillator; a 20 ppm crystal drifts ~1.7 s per day (20e-6 × 86,400), which is why unmonitored free-running clocks diverge in days.

## Common mistakes

- Specifying an oscillator class but not a holdover test.
- Sizing holdover from a datasheet instead of the repair time of the reference.
- Assuming holdover persists through a long power outage.
- Ignoring that the consumers' own oscillators drift too.
