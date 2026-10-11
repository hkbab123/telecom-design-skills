# Capacity Dimensioning

## Why it matters

Critical flows are tiny, so capacity planning is dominated by the performance and business traffic. The risk is not that voice fails for lack of bandwidth; it is that nobody planned how bulk traffic is limited when the cell fills.

## Method

1. **List flows per train and per fixed point** (from the KPI matrix, `02`): critical data and voice, on-board video, telemetry, diagnostics, passenger/business data.
2. **Count the worst-case simultaneous load per cell**: trains in the cell at once (headway, station stops, depot throats, overlapping coverage of adjacent tracks), including trains stopped in a station that share the same cell.
3. **Convert to uplink and downlink demand per cell**; with TDD, match against the configured uplink/downlink split.
4. **Estimate usable cell capacity** from bandwidth, spectral efficiency under realistic conditions (train speed, edge-of-cell, body loss), and overhead.
5. **Compare, then decide**: add a carrier, reduce site spacing, limit non-critical flows by policy, offload to another bearer, or accept degraded performance traffic.

## Worked example (illustrative figures)

Assumptions: 10 MHz TDD carrier, average spectral efficiency 1.5 bit/s/Hz, uplink share 30%.

- Usable cell throughput ≈ 1.5 × 10 = 15 Mbit/s total; uplink ≈ 0.3 × 15 = 4.5 Mbit/s.
- Demand: two trains in the cell, each uploading four CCTV streams at 1 Mbit/s → 8 Mbit/s uplink.
- Critical flows: per train, ETCS data and voice ≈ tens of kbit/s → under 0.2 Mbit/s for two trains.

Result: the video demand (8 Mbit/s) exceeds uplink capacity (4.5 Mbit/s) by almost 2×, while critical flows need about 4% of it. Without policy, congestion will hit everything in the cell; with priority and rate limits, critical flows are unaffected and video is throttled or moved to another bearer (e.g., station Wi-Fi at stops).

## Design levers

- Uplink-friendly TDD configuration, additional carrier, denser sites.
- **Policy:** video only at certain places or at lower quality; video buffered on board and uploaded at stations or depots.
- **QoS and admission control** so critical flows always find resources (`02`).
- **Multi-bearer offload** (`11`).

## Growth

Specify the growth horizon and headroom: new applications (ATO, remote diagnostics, richer video) are the likeliest source of demand growth. Re-run the worked calculation at the end of the horizon.

## Common mistakes

- Dimensioning from average traffic rather than the worst simultaneous cell.
- Forgetting trains stopped at stations still consume cell capacity.
- Assuming spectral efficiency of a static user for a train at speed.
- No policy for non-critical traffic.
