# 5G NR and LTE Radio for Rail

## Why it matters

The radio choices (duplex mode, carrier bandwidth, antenna configuration, numerology) set the coverage, capacity and mobility behaviour. Railway use is unusual: long linear coverage, trains at high speed with penetration loss through carriage bodies, and tunnels.

## Basics an FRMCS designer must know

- **LTE** is an early bearer for FRMCS-capable services and bridging; **5G NR** is the target. Both are specified in 3GPP radio series (TS 36, TS 38).
- **Duplex mode** — FDD uses paired frequencies for uplink and downlink; TDD uses one band and alternates in time. TDD requires tight phase synchronisation between all cells (`14`) and a chosen uplink/downlink ratio that suits the traffic (railway uplink-heavy demand from video and telemetry argues for attention to this ratio).
- **Carrier bandwidth** — wider carriers carry more traffic; the available spectrum fixes the choice (`05`).
- **MIMO and beamforming** — improve spectral efficiency and cell-edge performance; on a high-speed train they behave differently from static users because the channel changes rapidly.
- **Subcarrier spacing / numerology (NR)** — wider spacing is more tolerant of Doppler spread; a high-speed deployment must verify the chosen numerology against train speed.
- **Linear cell layout** — most cells see a train arriving, passing and leaving. Antennas are directional along the track, with back-to-back sectors or one-sector-each-way layouts.

## Doppler worked example

Doppler shift = (speed ÷ speed of light) × carrier frequency.

| Speed | At 0.9 GHz | At 1.9 GHz |
|---|---|---|
| 350 km/h (97.2 m/s) | ≈ 292 Hz | ≈ 616 Hz |
| 500 km/h (138.9 m/s) | ≈ 417 Hz | ≈ 880 Hz |

The shift reverses sign as the train passes the site, so the receiver sees a swing of about twice that value (≈ 1.2 kHz at 350 km/h and 1.9 GHz). Receivers must track this; wider subcarrier spacing and robust frequency-offset correction handle it. Single-frequency networks with radio heads positioned along the track can reduce the number of Doppler sign changes; this is a vendor-solution topic to confirm with the OEM.

## Penetration and antenna

Carriage body loss (often several dB to above 20 dB, depending on construction and window coating; illustrative) must be included in the link budget (`06`). The roof-mounted on-board antenna avoids the carriage loss for the cab link; the antenna placement is a design item (`11`).

## Design decisions

1. Duplex mode and uplink/downlink ratio per the spectrum position.
2. Carrier bandwidth, MIMO configuration and numerology validated for maximum speed.
3. Sector layout along the track.
4. Whether to use remote radio heads and distributed layouts.

## Common mistakes

- Copying a public-network radio template onto a high-speed corridor without checking Doppler and handover.
- Ignoring the TDD frame configuration's effect on uplink capacity.
- Leaving carriage penetration loss out of the budget.
