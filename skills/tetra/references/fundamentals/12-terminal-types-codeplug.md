# Terminal Types, Radio Architecture & Codeplug/Provisioning

What actually determines which talkgroups a radio can use and why "just reprogram it" isn't trivial at fleet scale.

## Terminal categories

- **Handheld (portable)** — carried by a person, battery-powered, lowest TX power (RF power class dependent — commonly in the low-watt range, confirm actual figure with OEM), the terminal type most exposed to hazardous-area certification requirements (see fundamentals file 18) since it physically enters classified zones.
- **Mobile (vehicle-mounted)** — installed in a vehicle, powered from the vehicle electrical system, generally higher TX power than a handheld (larger antenna, no battery-life constraint), used for vehicle-based field crews or as a DMO gateway platform.
- **Fixed/desktop** — control-room or fixed-location terminals, often paired with a dispatcher console rather than used standalone.
- **Covert/specialist variants** — exist in the market for specific security use cases; out of scope for a general design unless the client specifically requires it.

Each category has its own RF power class, battery/power characteristics, and — critically for O&G — its own ATEX/IECEx certification status (a handheld certified for a given zone is a specific certified product variant, not a generic feature toggled on any handheld).

## The codeplug concept

A **codeplug** is the configuration data loaded into a terminal that defines its operational behaviour: which talkgroups it's a member of, its scan list, its individually-addressable identity (ISSI — Individual Short Subscriber Identity), emergency-button behaviour, encryption keys (initial provisioning, before OTAR takes over ongoing rekeying), and channel/network parameters. This is programmed via the OEM's own fleet-management/programming software — a vendor-specific tool, not something this skill can detail beyond the concept.

## Why "just reprogram it" isn't trivial

At fleet scale (tens to hundreds of terminals), codeplug management is itself an operational process: a change to talkgroup structure (e.g. adding a new group, per Stage 2 item 6) means every affected terminal's codeplug needs updating, either individually via the OEM's programming tool/cable, or — for parameters within its scope — via OTAR/over-the-air provisioning where the network and terminal support it. This is why talkgroup/fleet-mapping design (Stage 2 item 6) should be treated as a genuinely deliberate, hard-to-change-later decision, not something to leave loose and adjust casually post-deployment.

## Why this matters for design decisions

- Every terminal in a hazardous-area deployment must be the specific ATEX/IECEx-certified product variant for its intended zone — a "regular" handheld of the same model line is not automatically certified; confirm the exact certified part number with the OEM (Stage 2 item 2/9).
- Fleet mapping and DGNA design (fundamentals file 07) should anticipate how much post-deployment flexibility the client actually needs, since anything beyond DGNA's dynamic scope requires a codeplug update process.
- ISSI assignment (each terminal's unique network identity) is a fleet-management detail usually handled by the OEM/integrator during commissioning — worth flagging as a Stage 3 deliverable item (terminal inventory/ISSI register) even though the current Stage 3 sequence doesn't call it out explicitly.

Formal reference: no single ETSI standard covers codeplug format (it's vendor-specific); ISSI addressing is defined in ETSI EN 300 392-2.
