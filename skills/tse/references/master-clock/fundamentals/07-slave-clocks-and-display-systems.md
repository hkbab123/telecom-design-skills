# Slave Clocks and Display Systems

## Why it matters

Clocks are the most visible output of a master clock: passengers and staff read them, and a clock that disagrees with the next one down the platform destroys confidence in the whole system. Display clocks should not be treated as an afterthought to the time-server design.

## Types

- **Analogue** — impulse-driven or IP-driven movement; familiar and robust, but slower to recover after a fault.
- **Digital** — LED/LCD, synchronised over NTP/PTP/PoE or a serial line; can show the time zone, date, and a fault indication.
- **Combination or station displays** — time shown alongside train information on passenger information displays; the time source for these should be the master clock, not each display's own source.
- **Control room clocks** — often show UTC plus local time, sometimes several zones.

## Synchronisation method

| Method | Notes |
|---|---|
| IP clock (NTP, optionally PoE) | Simplest wiring, easy to monitor, relies on network availability |
| Impulse line | Legacy; no time-of-day check (see `06`) |
| Serial/RS-485 time line | Needs addressing and a polling master |
| Wireless/RF time distribution | Useful in refurbishment; add RF survey and licensing check |

## Design decisions

1. **Failure behaviour** — what a clock shows when it loses sync: keep showing (risky), show a "no sync" marker, blank, or switch to an alarm state. A visibly wrong clock is worse than a visibly broken one; specify it.
2. **Daylight saving and zone changes** — specify who applies it (master or clock) and how every clock changes at the same instant.
3. **Accuracy and agreement** — a stated maximum difference between clocks that a passenger can see side by side; 1 s is commonly adequate for display, but set it in the spec.
4. **Readability** — character or dial size is sized to the maximum viewing distance and lighting, per the client's passenger-information guidelines.
5. **Environmental and vandal rating** — outdoor and platform clocks need suitable ingress (IP) and impact (IK) ratings (IEC 60529, IEC 62262) and temperature range; for the rail platform edge, also consider cleaning and mounting height.
6. **Hazardous areas** — a clock inside a classified area must be certified for the zone (rare in control rooms but possible on plant).
7. **Power** — PoE or a UPS-backed supply; consider what the clock shows during a long outage.
8. **Maintenance** — status reporting to the NMS (sync state, last sync, battery for any internal backup) so a failed clock is found by the system, not by a passenger.

## Common mistakes

- Clocks fed from different sources in adjacent areas.
- Clocks that silently freeze or free-run on loss of sync.
- Daylight-saving change applied by individual devices at different moments.
- No status monitoring of the clocks themselves.
