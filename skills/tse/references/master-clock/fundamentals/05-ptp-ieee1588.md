# PTP (IEEE 1588)

**Technical basis for Rule 5:** PTP reaches microsecond and better accuracy only if the network is designed for it, and asymmetry is the main enemy.

## Why it matters

When a consumer needs better than NTP can reliably give (sub-millisecond to microsecond, e.g. sequence of events, substation protection), PTP is the main network-delivered option. It achieves that by using hardware timestamping and by having the network equipment itself take part.

## Roles

- **Grandmaster** — the clock the rest follow, normally GNSS-disciplined. A **best master clock algorithm (BMCA)** chooses it automatically from announce messages (priority, clock class, accuracy).
- **Ordinary clock** — an end device, master or slave.
- **Boundary clock (BC)** — a switch that terminates PTP on the upstream port and regenerates it downstream, so each hop is a fresh, short, measured path.
- **Transparent clock (TC)** — a switch that forwards PTP and corrects the message for the time it spent inside (residence time). Peer-to-peer TCs also measure link delay.

## Profiles

A profile fixes the options so devices interoperate.

| Profile | Use |
|---|---|
| Default (IEEE 1588) | General purpose |
| ITU-T G.8275.1 | Phase/time in telecom, full on-path support, usually with SyncE assistance |
| ITU-T G.8275.2 | Phase/time with partial on-path support, over IP |
| ITU-T G.8265.1 | Frequency only |
| Power profile (IEC/IEEE 61850-9-3, IEEE C37.238) | Substation automation, requires microsecond-level accuracy over a defined hop count |
| gPTP (IEEE 802.1AS) | Time-sensitive networking and AV |

A device and its network must use the same profile; say which in the spec.

## Asymmetry

PTP, like NTP, assumes the forward and return paths take equal time. The time error caused by asymmetry is half of the asymmetry.

**Worked example:** two fibres in a pair differ by 100 m in length (for instance, routed through different cross-passages). Fibre delays ~5 ns/m, so path asymmetry ≈ 500 ns and the time error ≈ 250 ns at that hop. Hops add. Wavelength-dependent delay on single-fibre bidirectional links adds another asymmetry unless it is calibrated.

## Design decisions

- **Full on-path support** (every switch a BC or TC) gives the best result; a single non-PTP-aware switch can add large, variable error through queuing.
- **Limit hop count** to what the budget allows; power-profile accuracy is defined over a stated number of hops.
- **Dedicate** VLAN and QoS priority to PTP; keep it off paths with variable load.
- **Reject rogue masters** with port roles configured (master-only/slave-only) and priority settings so a stray device cannot take over (`14`).
- **Timescale** — PTP is TAI-based; make sure the UTC offset and leap-second flags are consumed correctly by every slave (`01`).
- **Asymmetry calibration** — measure or document fibre length differences and equipment latency at commissioning (`15`).

## Common mistakes

- Using PTP over a network with unaware switches and expecting microsecond accuracy.
- Mixing profiles on one network.
- Ignoring asymmetry from unequal fibre length or SFP delay.
- Allowing any device to become grandmaster.
