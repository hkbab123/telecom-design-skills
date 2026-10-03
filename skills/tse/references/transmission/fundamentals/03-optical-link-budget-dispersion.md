# Optical Link Budget and Dispersion

**Technical basis for Rule 3:** budgets are computed at end-of-life, not day one.

## Loss budget method

```
Span loss = (fibre length × attenuation coefficient)
          + (splice count × splice loss)
          + (connector count × connector loss)
          + repair allowance
          + ageing/temperature allowance
          + operating margin
```

Compare against the **power budget** of the interface: transmitter launch power minus receiver sensitivity (with the receiver's overload limit respected).

## Illustrative values (verify against project spec and vendor data)

- Attenuation at 1310 nm ≈ 0.35 dB/km; at 1550 nm ≈ 0.20–0.25 dB/km (G.652 class fibre).
- Fusion splice ≈ 0.05–0.1 dB; mechanical connector pair ≈ 0.3–0.5 dB.
- Repair allowance: reserve for several future repair splices per span (e.g. 0.1 dB each, number set by route risk).
- Operating margin: typically a few dB; policy decision by client/designer.

### Worked example (illustrative)

A 40 km span at 1550 nm: 40 × 0.25 = 10 dB fibre; 10 splices × 0.1 = 1 dB; 2 connector pairs × 0.5 = 1 dB; repair/ageing 2 dB; margin 3 dB. Total ≈ 17 dB. If the chosen interface offers a 20 dB budget the span passes with 3 dB of headroom, and the check is repeated at the worst-case (end-of-life) values to confirm.

## Dispersion

- **Chromatic dispersion (CD)** — different wavelengths travel at different speeds; limits high-rate, long spans; compensated by dispersion-compensating modules or coherent receivers.
- **Polarisation mode dispersion (PMD)** — random, grows with the square root of length; matters for ≥10 Gb/s over older fibre or very long spans.
- At rail/O&G distances (typically tens of km per span at ≤10 Gb/s) dispersion rarely limits; it matters on DWDM or very long spans (see `06`).

## OSNR (for amplified/DWDM systems)

In amplified links the limit is optical signal-to-noise ratio, not just loss; each amplifier adds noise. See `06-otn-dwdm-cwdm.md`.

## Common mistakes

- Using datasheet "typical" fibre loss without margin for the oldest or worst section.
- Ignoring existing joints in re-used/third-party fibre.
- Forgetting to check receiver overload on short spans (needs an attenuator).
