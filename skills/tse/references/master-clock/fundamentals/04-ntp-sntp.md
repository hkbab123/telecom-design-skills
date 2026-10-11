# NTP and SNTP

**Technical basis for Rule 5:** accuracy at the consumer is bounded by the path, not just the source.

## Why it matters

NTP is the default time protocol for IT and most OT consumers. It is cheap and everywhere, but its accuracy depends on the network path and the quality of the client implementation. Specifying "NTP" without an accuracy at the consumer says almost nothing.

## How it works

- **Stratum** — distance from a reference: stratum 0 is the reference (GNSS, atomic), stratum 1 a server directly attached to it, stratum 2 syncs to stratum 1, and so on. Accuracy generally degrades with each level.
- A client exchanges timestamped packets with a server and computes offset and round-trip delay. It **assumes the forward and return delays are equal**.
- A full **NTP** client (RFC 5905) polls several servers, filters samples and discards inconsistent ones ("falsetickers"). **SNTP** (RFC 4330) is a simple client: it takes the time from one server with no such selection and no discipline of the local clock. Many embedded devices are SNTP-only.

## Accuracy envelope

The offset error is bounded by half the round-trip delay (the unknown asymmetry could be all on one leg).

**Worked example:** round-trip delay 20 ms → offset error up to ±10 ms in the worst case. On a quiet, switched local network with small and symmetric delay, typical results are far better (sub-millisecond to a few milliseconds, depending on implementation and load, illustrative); over a WAN or a satellite link the bound grows, and asymmetry (as on a geostationary VSAT link) can make it much worse. Hardware timestamping in the NIC and server improves LAN accuracy markedly.

## Design implications

- **Use several servers** for full NTP clients so a bad one can be outvoted. Three is the minimum that allows one to be outvoted; more is better. An SNTP-only consumer should point at a master clock designed as its single trusted source, with redundancy provided by the master pair (`08`).
- **Step vs slew** — small offsets are slewed gradually; large offsets are stepped. Define the threshold, and decide what each consumer does on a step (some applications and databases misbehave when time jumps backwards).
- **Poll interval** — shorter intervals track drift better at the cost of load.
- **Authentication** — symmetric keys or **Network Time Security (NTS, RFC 8915)** protect against a spoofed server. Support differs by consumer; list which consumers can authenticate (`14`).
- **Broadcast/multicast modes** reduce load on large networks but give up the delay measurement and so degrade accuracy.
- **No public servers** — consumers must not be allowed to fall back to a public internet pool; it breaks Rule 4 and the security boundary.

## Common mistakes

- Treating "NTP-synchronised" as meaning a specific accuracy.
- One server for a full NTP client (no protection against a faulty source).
- Letting a consumer pick its own public servers.
- Using NTP across a satellite link and expecting millisecond results.
- Not telling application owners that time can step.
