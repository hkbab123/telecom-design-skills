# Terminal Types, Radio Architecture & Codeplug/Provisioning

What actually determines which talkgroups a radio can use and why "just reprogram it" isn't trivial at fleet scale.

## Terminal categories

- **Handheld (portable)** — carried by a person, battery-powered, lowest TX power (RF power class dependent — commonly in the low-watt range, confirm actual figure with OEM), the terminal type most exposed to hazardous-area certification requirements (see fundamentals file 18) since it physically enters classified zones.
- **Mobile (vehicle-mounted)** — installed in a vehicle, powered from the vehicle electrical system, generally higher TX power than a handheld (larger antenna, no battery-life constraint), used for vehicle-based field crews or as a DMO gateway platform.
- **Fixed/desktop** — control-room or fixed-location terminals, often paired with a dispatcher console rather than used standalone.
- **Covert/specialist variants** — exist in the market for specific security use cases; out of scope for a general design unless the client specifically requires it.

Each category has its own RF power class, battery/power characteristics, and — critically for O&G — its own ATEX/IECEx certification status (a handheld certified for a given zone is a specific certified product variant, not a generic feature toggled on any handheld).

## Environmental ruggedisation — the general baseline before EN 50155

Every terminal category, not just rail-onboard equipment, is specified against a baseline environmental/ruggedisation test regime — temperature range (operating and storage, typically wider for storage than operating), humidity, vibration, and shock, each tested to a referenced standard class (commonly drawn from the ETS 300 019 environmental-class series, or an equivalent standard the OEM tests against), plus an **ingress protection (IP) rating** per IEC 60529 (e.g. IP54 for splash/dust resistance suited to a dispatcher console or vehicle radio, IP64 or higher for a handheld expected to handle sand/dust and heavier water exposure in field/outdoor use). Confirm the specific classes and IP rating against the OEM's datasheet for the actual product being specified — these figures vary by terminal category and by OEM, but the requirement to state them explicitly (not leave environmental suitability implicit) belongs in Stage 2/3 equipment specification regardless of category.

## Environmental ruggedisation — EN 50155 and equivalent (onboard rail equipment specifically)

Cab radios and other onboard train equipment sit in an environment general handheld/mobile terminal ratings don't cover: continuous vibration and shock from the moving vehicle, and a wider ambient temperature range than a typical vehicle cab. **EN 50155** is the railway-specific standard for electronic equipment used on rolling stock, covering exactly this — defined vibration/shock test profiles, extended temperature ranges, and power-supply-variation tolerance (rail vehicle DC supplies fluctuate more than a stable mains-derived supply). A terminal or onboard gateway/repeater unit intended for permanent installation on rolling stock should be the specific EN 50155-qualified product variant, not a general mobile terminal simply bolted into a cab — the same principle as ATEX/IECEx certification above (fundamentals file 18): the certification attaches to a specific tested product, not a general model line, so confirm the exact qualified part number with the OEM rather than assuming a mobile-category terminal automatically qualifies for permanent rail-vehicle installation.

## Audio accessories and noise environments

Standard terminal audio (built-in speaker/microphone) is often inadequate in the specific high-noise environments common to rail and O&G operations — compressor stations, heavy track-tamping machinery, and similarly loud plant/trackside equipment can push ambient noise well past the point where a standard microphone captures intelligible speech or a standard speaker is audible. Accessory options worth scoping explicitly where the operational environment demands it, rather than assumed adequately covered by a standard handset:
- **Heavy-duty/noise-cancelling headsets and ear defenders** — combine hearing protection (a workplace-safety requirement in its own right in high-noise areas) with a noise-cancelling or noise-cancelling-adjacent microphone.
- **Throat microphones** — pick up speech via vibration at the throat rather than airborne sound, largely immune to ambient acoustic noise, common in extreme-noise or confined-space/breathing-apparatus use cases.
- **Bone-conduction earpieces** — transmit audio via bone vibration rather than through the ear canal, useful where hearing protection or breathing apparatus makes a conventional earpiece impractical, or where situational awareness of surrounding ambient sound needs to be preserved alongside radio audio.

Where accessories are used in a classified hazardous area, they inherit the same ATEX/IECEx certification requirement as the terminal itself (fundamentals file 18) — an otherwise-suitable accessory that isn't itself certified for the zone can't legitimately be paired with a certified handheld for use in that zone, so accessory certification status needs the same confirm-with-OEM discipline as the terminal itself.

## Numbering schemes — how a terminal is actually addressed

Beyond the ISSI (below), a TETRA deployment needs a consistent **numbering scheme** so terminals can be addressed and identified consistently across the network and by any interconnected system (PABX/PSTN, per fundamentals file 20):
- **Subscriber Identity Numbering** — the terminal's underlying network identity (the ISSI itself, and the associated individual/group short subscriber identities the SwMI uses internally for routing).
- **Fleet-Specific Short Numbering** — a shorter, operationally meaningful numbering plan layered on top of the underlying network identities, structured around the client's own fleet/organisational logic (e.g. a numbering block per depot, per shift team, or per vehicle type) so dispatchers and field users work with numbers that mean something operationally, rather than raw network identities.
- **MSISDN-style numbering** — where the network interconnects with PABX/PSTN telephony (fundamentals file 20), a terminal may also need an ISDN-style dialable number for that interconnect, distinct from its native TETRA identity, following the same PABX/PSTN numbering plan any other extension on that PABX uses.

The network also typically supports displaying the calling party's number/alias on the receiving terminal's screen — a usability feature worth confirming works as expected with the client's chosen numbering scheme during Stage 3 testing, not assumed automatic. Numbering-scheme design should happen alongside talkgroup/fleet-mapping design (Stage 2 item 6) — it's the addressing layer underneath that decision, not a separate afterthought.

## The codeplug concept

A **codeplug** is the configuration data loaded into a terminal that defines its operational behaviour: which talkgroups it's a member of, its scan list, its individually-addressable identity (ISSI — Individual Short Subscriber Identity), emergency-button behaviour, encryption keys (initial provisioning, before OTAR takes over ongoing rekeying), and channel/network parameters. This is programmed via the OEM's own fleet-management/programming software — a vendor-specific tool, not something this skill can detail beyond the concept.

## Why "just reprogram it" isn't trivial

At fleet scale (tens to hundreds of terminals), codeplug management is itself an operational process: a change to talkgroup structure (e.g. adding a new group, per Stage 2 item 6) means every affected terminal's codeplug needs updating, either individually via the OEM's programming tool/cable, or — for parameters within its scope — via OTAR/over-the-air provisioning where the network and terminal support it. This is why talkgroup/fleet-mapping design (Stage 2 item 6) should be treated as a genuinely deliberate, hard-to-change-later decision, not something to leave loose and adjust casually post-deployment.

## Why this matters for design decisions

- Every terminal in a hazardous-area deployment must be the specific ATEX/IECEx-certified product variant for its intended zone — a "regular" handheld of the same model line is not automatically certified; confirm the exact certified part number with the OEM (Stage 2 item 2/9).
- Fleet mapping and DGNA design (fundamentals file 07) should anticipate how much post-deployment flexibility the client actually needs, since anything beyond DGNA's dynamic scope requires a codeplug update process.
- ISSI assignment (each terminal's unique network identity) is a fleet-management detail usually handled by the OEM/integrator during commissioning — worth flagging as a Stage 3 deliverable item (terminal inventory/ISSI register) even though the current Stage 3 sequence doesn't call it out explicitly.

Formal reference: no single ETSI standard covers codeplug format (it's vendor-specific); ISSI addressing is defined in ETSI EN 300 392-2.
