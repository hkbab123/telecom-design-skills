# Migration Path — FRMCS/LTE-R Technical Basis

The technology direction behind Design Rule 4 ("Design for FRMCS") — read this when the question is "what does FRMCS actually change technically, and how does that shape a GSM-R design decision today."

## Why GSM-R is being phased out

GSM-R is built on 2G GSM/GERAN technology (fundamentals file 01), which is being sunset industry-wide as mobile network operators refarm 2G spectrum for newer technologies — meaning long-term equipment availability, vendor support, and spectrum coexistence all trend unfavourably for GSM-R over the coming years, independent of any railway-specific driver. On top of this general 2G-sunset pressure, GSM-R's inherited 2G limitations (data throughput ceiling from GPRS/EDGE, fundamentals file 08; cryptographic weaknesses, fundamentals file 10) increasingly constrain what railway operators can do with the network, particularly around higher-bandwidth applications and stronger security postures.

## FRMCS — the replacement architecture

Future Railway Mobile Communication System, standardised through UIC-led international rail industry work, is LTE-based (with a path toward 5G) rather than GSM-based — a fundamentally different air interface and core architecture (packet-switched throughout, not GSM's circuit-switched-voice-plus-GPRS-data hybrid), analogous in spirit to how public mobile networks moved from 2G/3G to 4G/5G, but designed specifically around railway's safety-relevant and mission-critical communication needs (successor mechanisms to eMLPP priority, VGCS group calls, and functional addressing — fundamentals files 07/11 — reimagined for an LTE/5G bearer, generally under the banner of Mission-Critical Services standards, MCX, from 3GPP).

## What "FRMCS-ready" actually means for a GSM-R design today

Since GSM-R and FRMCS use fundamentally different radio technology (not a simple software upgrade), "FRMCS-readiness" in a present-day GSM-R design is mostly about **avoiding decisions that would obstruct a later parallel or phased FRMCS rollout**, rather than any GSM-R equipment itself becoming FRMCS-capable:
- **Site infrastructure reusability** — trackside sites (masts, cabinets, power, backhaul — fundamentals files 13/14/16) chosen/dimensioned with enough capacity/space margin that they could later host FRMCS radio equipment alongside or in place of GSM-R equipment, rather than needing entirely new civil works.
- **Backhaul capacity margin** — fibre backhaul (fundamentals file 14) dimensioned with headroom, since FRMCS's LTE/5G-based data services will have materially higher bandwidth requirements than GSM-R's GPRS/EDGE ceiling.
- **Operational transition planning** — for a long-lived project (rail infrastructure decades-long lifecycle), the client's own FRMCS transition timeline/strategy (if one exists) should shape whether the GSM-R design is explicitly scoped as an interim/bridge system with a defined transition horizon, versus a full-lifecycle asset — this is a client strategic decision to surface explicitly (Stage 1/2), not a technical GSM-R design choice to make unilaterally.

## Why this matters for design decisions

- Site civil works and backhaul dimensioning are the two most concrete places a present-day GSM-R design can meaningfully ease a future FRMCS rollout — worth raising explicitly at Stage 1/2 rather than treating FRMCS as someone else's future problem.
- The client's own FRMCS transition strategy and timeline (if defined) should be asked about explicitly at Concept/Tender stage, since it materially affects whether the GSM-R network is designed as a long-lifecycle asset or a bridge system — don't assume either without asking.
- This is a genuinely fast-moving standards area — treat the specifics of FRMCS/MCX standardisation status as needing a current check against UIC/3GPP sources for any live project, not something this file's summary should be relied on as definitive for.

Formal reference: UIC FRMCS specification set (functional/system requirements); 3GPP Mission-Critical Services (MCX) standards (the underlying LTE/5G mechanisms FRMCS builds on).
