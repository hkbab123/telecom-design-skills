# Time Fundamentals: UTC, GNSS Time and Traceability

**Technical basis for Rule 6:** define the time policy once.

## Why it matters

"The same time everywhere" hides several different questions: which timescale, which zone, how leap seconds and daylight saving are handled, and traceable to what. Two systems can both be "synchronised" and still disagree by 18 seconds or an hour because they made different choices.

## Terms that get confused

- **Time-of-day** — a date and clock reading (what a log line or a wall clock shows).
- **Frequency** — how fast a clock ticks. Matters to TDM transport and radio; not the same as knowing the time.
- **Phase / time error** — the offset between two clocks' ticks. Matters to TDD radio and sample-aligned measurement.
- **Accuracy** — closeness to the reference (UTC). **Precision/stability** — how consistent a clock is with itself. A stable clock can be consistently wrong.

## Timescales

- **UTC** — the civil timescale, kept within about 0.9 s of Earth rotation by occasional leap seconds.
- **TAI** — atomic time, no leap seconds; ahead of UTC by 37 s (value since the 31-Dec-16 leap second; verify the current value).
- **GPS time** — started 06-Jan-80, no leap seconds, so it runs ahead of UTC by 18 s (same caveat). Other constellations use their own scales with their own offsets; a receiver converts using the navigation message.
- **PTP time** — a TAI-based timescale; the announce message carries the current UTC offset so a consumer can convert.

## Leap seconds and daylight saving

- A positive leap second inserts 23:59:60. Many systems cannot represent it; they step, repeat a second, or "smear" it across hours. The policy must be chosen once and applied to every consumer, or logs will disagree across the event. International bodies have resolved to stop leap seconds by or before 2035; check the current position when writing a long-life spec.
- Keep system clocks and logs in **UTC**; apply the time zone and daylight saving only at the display layer. This avoids the ambiguous repeated hour when daylight saving ends. Where a region observes no daylight saving, still specify UTC-based logs so equipment from other regions behaves identically.

## Worked example: GPS to UTC

A receiver outputs GPS-time stamp 12:00:18. With the GPS–UTC offset at 18 s, UTC is 12:00:00. A consumer that uses the raw GPS stamp as UTC is 18 s off; that is an easy-to-miss configuration error when a receiver's output mode is changed.

## Traceability chain

National time laboratory (UTC(k)) → GNSS constellation → timing receiver → master clock → sub-masters → consumers. A claim of "traceable to UTC" needs this chain to be documented, with the uncertainty at each step; when GNSS is lost, traceability continues only in the sense of a bounded, stated drift (see `03-oscillators-holdover.md`).

## Common mistakes

- Logging in local time with daylight saving and then correlating events across the transition.
- Mixing GPS time and UTC in one system.
- Not specifying leap-second handling, then discovering consumers disagree after the next one.
- Calling a system "synchronised" without stating to what accuracy at the consumer.
