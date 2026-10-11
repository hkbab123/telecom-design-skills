# O&G: Plant Time, Sequence of Events, Substations and Remote Sites

## Why it matters

After a trip, release or fire, the incident investigation depends on the order of events across DCS, ESD, fire & gas, electrical protection and CCTV. A millisecond-level event timeline needs deliberate design; a plant where every system is "roughly right" cannot establish what happened first.

## Where time is consumed

- **DCS / SCADA** — alarm and event stamping, historian records; often ~1 to 10 ms from NTP or from the DCS vendor's own time distribution.
- **SIS / ESD / F&G** — sequence-of-events (SOE) cards stamp changes at the I/O card to ~1 ms; typically fed by IRIG-B, 1PPS or PTP from the master clock. The SIS must keep its independence from SCADA (see `references/scada`); time distribution into the SIS should be one-way and designed with the SIS engineer.
- **Electrical substations** — protection relays and IEC 61850 devices; PTP power profile (IEC/IEEE 61850-9-3) or IRIG-B, microsecond-scale for sampled values and synchrophasors.
- **Pipeline SCADA** — leak-detection systems compare time-aligned flow and pressure from separated stations; clock skew between RTUs degrades the comparison.
- **CCTV, PAGA, PABX, enterprise IT** — as in rail (`09`).

## Hazardous areas

- Place GNSS antennas and master clocks **outside classified zones** (safe area, roof of a control building) wherever possible and bring time into the zone over certified cabling or fibre; where equipment must be inside a zone, it needs certification (IEC 60079 series, ATEX/IECEx) *for the specific model and zone*, not just the family.
- Certification is attached to the product variant: confirm it for the chosen unit, not the manufacturer's range.

## Offshore and remote sites

- Platform structure and flare can shadow or interfere with the antenna; survey the siting.
- Remote or pipeline sites often have long, narrow-bandwidth or satellite links to the control centre. NTP over a geostationary satellite link has long, asymmetric delay and poor accuracy (`04`); give those sites **their own GNSS-disciplined time source** rather than synchronising across the link.
- Where the site has no GNSS (rare) or its use is restricted, document the fallback and its accuracy limits.

## Tie-back to incident analysis

For a trip investigation define up front: the single time reference all systems use; the maximum allowed difference between SOE-stamped events across systems; where each system's clock status is logged. This is what turns a master clock into evidence.

## Common mistakes

- Separate DCS vendors each keeping their own time and a different offset.
- GNSS antenna placed where it needs hazardous-area certification.
- Satellite-linked sites depending on NTP across the link.
- Time distribution into the SIS that creates a path from SCADA into the protection layer.
