# Backhaul, Transport and Synchronisation

## Why it matters

Every radio site depends on backhaul. If the backhaul is slow, shared without priority, or not synchronised, the FRMCS KPIs fail regardless of the radio design. TDD radio makes synchronisation a hard requirement.

## Backhaul

- **Medium** — fibre is the default along a railway corridor; microwave or leased circuits where fibre is not available. In tunnels, the backbone typically runs on the trackside fibre network.
- **Capacity** — the sum of the cell's peak traffic plus signalling and management, with growth headroom. 5G sites are higher-capacity than legacy sites, so legacy backhaul may be insufficient (`07`).
- **Latency** — adds to the end-to-end latency of the critical flows; fix a one-way delay budget per hop and per path.
- **Protection** — ring or dual-homed paths with true physical diversity (a logical ring in a shared duct is not diverse); see the `transmission` subsystem's physical-diversity rule.
- **QoS** — transport must preserve the priority of critical flows (marking, queues, policing) end to end.
- **Security** — encryption of the transport where the backhaul crosses untrusted or shared infrastructure (`16`).

## Synchronisation

- **Frequency** is needed by all radios; **phase/time** is needed by TDD cells to avoid interference between neighbouring sites' uplink and downlink.
- Common approaches: GNSS at each site (simple but vulnerable and unavailable in tunnels), or network-delivered timing using PTP telecom profiles (ITU-T G.8275.1 with full on-path support is common for phase), with SyncE for frequency (ITU-T G.8261/G.8262), from a primary reference time clock (ITU-T G.8272).
- **Holdover** — what the radio does when sync is lost; the TDD cell must stop transmitting or degrade gracefully before it interferes.
- **Tunnels** — no GNSS underground; timing must be carried by the transport.

## Relationship to other subsystems

- The `transmission` subsystem in this skill designs the transport network and its synchronisation architecture (including frequency/phase distribution); FRMCS states its requirements (capacity, latency, protection, phase accuracy) as inputs to that design.
- The `master-clock` subsystem handles time-of-day distribution to consumers; it is separate from radio phase synchronisation, though both may share a GNSS/PRTC reference. Define the boundary explicitly (see `18`).

## Worked check: phase budget

If the radio needs a phase accuracy of about ±1.5 µs at the antenna port (a commonly cited figure for some TDD configurations; confirm the exact figure for the product), the budget is split between the reference clock, each network element's error and any asymmetry. A fibre-length mismatch of 100 m between forward and return paths gives about 500 ns of asymmetry, hence ≈ 250 ns of time error at that hop. A chain of several such errors consumes a large part of the budget.

## Common mistakes

- Reusing legacy backhaul capacity.
- Specifying PTP but allowing non-PTP-aware switches in the path.
- Counting GNSS as the sole sync source in tunnels.
- No holdover behaviour specified for the radio.
