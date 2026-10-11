# Legacy Time Distribution: IRIG-B, 1PPS, Serial and Impulse Lines

## Why it matters

Plenty of existing RTUs, protection relays, sequence-of-events (SOE) modules and analogue slave clocks do not speak NTP or PTP. They take time on dedicated wires. A new master clock usually has to feed these for years, so the spec must say which legacy outputs are needed and how they are verified.

## IRIG-B

- A time code from the IRIG Standard 200 family, sent as one frame per second, normally carrying time of day, day of year and, in extended forms, year and time-quality information (the extensions are carried into IEEE C37.118).
- **Unmodulated (DC level-shift)** form is a logic-level signal good to roughly the microsecond region when well installed; **modulated (1 kHz carrier)** form travels better over longer or noisier runs but with coarser edge accuracy (illustrative; confirm with the receiving device's datasheet).
- Distributed from the master to consumers with **distribution amplifiers** and single-purpose cabling; each run's length adds propagation delay that matters only at the microsecond scale.

## 1PPS and time string

- A **one-pulse-per-second** signal marks each second boundary; a **serial time string** (for example an NMEA-style message over RS-232/RS-485) tells which second it is. A consumer needs both to be sure of time and phase.
- Common for GNSS-to-device links and for devices that need an accurate second edge.

## Impulse (minute-pulse) lines for analogue slave clocks

- Traditional slave clocks advance by electrical impulses, often a DC pulse each minute whose **polarity alternates** to step the movement forward. The master pulses all clocks together, so the line is a simple wired network of many clocks on a loop.
- Weak points: a broken loop or voltage drop leaves part of the network behind; there is no built-in time-of-day check, so clocks must be corrected by a command or resynchronisation sequence after a fault or power loss.
- New builds favour IP-based clocks (see `07`); impulse networks remain where analogue clocks are retained or for refurbishment.

## Design decisions

1. List every consumer on a legacy interface and its owner; ask what it really needs (the datasheet often supports several options).
2. Choose the signal and the amplifier arrangement; keep runs short and shielded; route away from power cables (rail traction EMC, `10`).
3. Decide which consumer is the time authority if it also feeds another (avoid cascades).
4. Verify at commissioning with a scope or interval counter, not by eye (`15`).

## Common mistakes

- Using a serial time string alone where a pulse edge is needed.
- Long unshielded IRIG runs near power cabling.
- Leaving the master's year or time-quality field wrong, so the relay rejects the code.
- Assuming a corrected impulse network self-corrects after power loss.
