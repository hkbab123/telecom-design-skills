# Accuracy Requirements by Consumer

**Technical basis for Rule 1:** the tightest consumer sets the requirement, not the clock.

## Why it matters

Accuracy is expensive: each step down (second → millisecond → microsecond) needs different protocols, network support and test equipment. Build the consumer matrix first and let it choose the architecture, rather than buying the best clock and discovering the network cannot carry its accuracy.

## Consumer matrix (illustrative figures; the client spec governs)

| Consumer | Typical need | Typical protocol |
|---|---|---|
| Passenger-facing and staff clocks | Visible agreement, ~1 s | NTP, impulse |
| Enterprise IT, directory services | Small fraction of the directory's allowed skew (e.g. Kerberos commonly tolerates 5 min by default) | NTP |
| CCTV recorders, PABX call records, PAGA logs | ~100 ms to 1 s so records can be correlated | NTP |
| SCADA/DCS alarms and event stamping | ~1 to 10 ms | NTP (best case) or PTP / IRIG-B |
| Sequence-of-events (SOE) modules, ESD/F&G | ~1 ms | IRIG-B, PTP, 1PPS |
| Protection relays, synchrophasors, IEC 61850 sampled values | ~1 µs | PTP power profile, IRIG-B |
| Radio TDD phase (transport domain) | Per ITU-T G.8271 classes, microsecond-scale | PTP telecom profile (see Transmission) |

## Worked example: budgeting for a 1 ms SOE requirement

Requirement: events from field I/O must be stamped within 1 ms of UTC.

| Contributor | Allocation (illustrative) |
|---|---|
| GNSS receiver to UTC | ~1 µs |
| Antenna cable delay (uncompensated residue) | ~1 µs |
| Distribution (PTP over a few hops, or IRIG-B) | ~10 to 50 µs |
| Consumer clock discipline and stamping resolution | 200 to 500 µs |
| Margin | remainder |

Observations: (1) NTP over a shared LAN cannot be relied on to meet 1 ms in all conditions, so PTP or IRIG-B is chosen; (2) the consumer's own resolution often dominates, so confirm it with the consumer's owner (stage 3, step 3); (3) the master's microsecond accuracy is irrelevant if the budget is spent downstream.

## How to build the matrix

1. List all consumers and ask the owner their need and their *actual* interface (what the device accepts, what it timestamps at).
2. Identify the tightest and any outliers; consider a second, separate distribution for the outlier rather than raising the whole system.
3. For each, work out end-to-end error with a budget sheet like the one above.
4. Confirm each consumer can *report* its sync state, or you cannot prove compliance.

## Common mistakes

- Specifying one accuracy for "the system".
- Taking the master's output accuracy as the accuracy at the consumer.
- Overlooking that a consumer's timestamp resolution is coarser than the stated need.
- Over-specifying microsecond accuracy for log correlation and paying for it.
