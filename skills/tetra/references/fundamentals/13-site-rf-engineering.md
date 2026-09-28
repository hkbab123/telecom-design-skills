# Site RF Engineering

The physical hardware layer behind the link budget (fundamentals file 04) and Stage 3's detailed design — read this when the question is "what actually sits at a base station site and why does it matter."

## Antenna systems

- **Antenna type and gain** — omnidirectional antennas spread coverage evenly around a site (typical for a single isolated site); directional/sector antennas concentrate energy toward a specific coverage area (typical for multi-sector sites serving a defined direction, e.g. covering one side of a plant or along a corridor). Higher gain concentrates energy into a narrower pattern — a design trade between coverage reach and pattern width, not a free efficiency gain.
- **Antenna height** — a major driver of coverage reach and line-of-sight to distant terminals; often more impactful on coverage than transmit power, especially in cluttered/industrial environments where height above surrounding structures matters more than raw power.

## Combiners and duplexers

At a multi-channel base station site, several transmitters often need to share one antenna. A **combiner** merges multiple transmit signals onto a shared feed with an associated insertion loss (a real dB figure that belongs in the link budget's "TX feeder/combiner loss" term — see fundamentals file 04). A **duplexer** allows simultaneous transmit and receive on a shared antenna (separating the two by frequency), also with its own insertion loss. Both are physical hardware choices with OEM-specific loss figures — always source the actual figure from the equipment datasheet, never assume a generic value.

## Feeder/cable loss

The cable run between the base station equipment and the antenna introduces loss proportional to cable length and frequency — longer runs (e.g. antenna on a tall mast, equipment at ground level) lose more signal before it even reaches the antenna. This is a real, calculable loss (cable-type-specific dB-per-metre figures from the cable manufacturer's datasheet) that belongs in the link budget, and is a reason to keep feeder runs as short as practical or to consider a tower-mounted amplifier where runs are unavoidably long.

## Passive Intermodulation (PIM), VSWR, and co-located-system interference

Beyond the linear loss figures above (combiner/duplexer/feeder loss), a site's RF hardware and its physical environment can generate genuine **interference**, not just attenuation — worth distinguishing as its own category of site engineering problem:

- **Passive Intermodulation (PIM)** — when two or more strong RF signals mix at a non-linear junction (a loose or corroded connector, dissimilar metals in contact, even rust on a nearby structure) and generate spurious signals at other frequencies, which can fall inside the receive band and raise the noise floor, degrading sensitivity without any obvious equipment fault. PIM is a particular risk in **highly metallic environments** — refineries, rail yards, ship/offshore structures — where the RF environment includes large amounts of loosely-bonded metalwork the designer doesn't directly control (a corroded handrail or loose flashing near an antenna can be a PIM source with no connection to the TETRA installation itself). Mitigated through low-PIM-rated connectors/cables at every joint, torque-spec'd connections, and, where the environment allows, site selection that keeps antennas clear of unrelated metallic structures. PIM is normally verified in the field with a dedicated PIM test set as part of commissioning (testing/commissioning fundamentals file), not something calculated in advance with confidence.
- **VSWR (Voltage Standing Wave Ratio)** — measures how well the antenna/feeder system is impedance-matched to the transmitter; a poor match reflects power back toward the transmitter instead of radiating it, wasting TX power (a link-budget loss) and, at extreme mismatch, risking transmitter damage. A maximum VSWR figure (e.g. a ratio such as 1.5:1) is a standard installation acceptance criterion, checked with a VSWR/return-loss meter at commissioning — an OEM-specified limit to confirm, not a universal constant.
- **Co-located-system interference (intermodulation studies)** — where a TETRA site shares a mast/rooftop with other radio systems (marine VHF at a port facility, legacy GSM-R at a rail site, commercial LTE at a shared tower), the combination of transmitters can generate intermodulation products landing on TETRA's receive frequencies, or vice versa degrading the other system. A formal **intermodulation study** — modelling the specific combination of frequencies, power levels, and antenna separation actually present at that shared site — is the standard mitigation-planning exercise for any genuinely multi-tenant site, typically followed by physical mitigation (increased antenna separation, custom cavity filters/duplexers tuned to reject the specific interfering frequencies) where the study flags a real risk. This is a site-specific engineering exercise, not something addressed generically in a technical specification — flag any shared/multi-tenant site explicitly for its own intermodulation study rather than assuming standard filtering is sufficient.

## Site layout considerations

- **Rack/cabinet siting** — equipment needs power, cooling, and physical protection (weatherproof cabinet for outdoor/remote sites, especially relevant for exposed O&G field locations).
- **Grounding/lightning protection** — masts and outdoor equipment need proper earthing and lightning protection, a standard telecom site-engineering practice, more safety-critical in exposed field/offshore O&G locations.
- **Hazardous-area siting (O&G)** — even where the base station equipment itself sits outside the classified zone, antenna/cabling that enters or passes near a classified zone triggers the same certification/installation-practice requirements covered in fundamentals file 18 — site layout should aim to keep RF equipment outside classified zones wherever coverage requirements allow.

## Why this matters for design decisions

- Every antenna/combiner/duplexer/feeder loss figure feeds directly into the link budget calculation (fundamentals file 04) — Stage 3's "detailed link budget" (item 7) is only as accurate as the real, OEM-sourced loss figures used here, not the illustrative example numbers.
- Antenna height and directionality choices are often a more cost-effective way to improve coverage than increasing transmit power — worth considering before assuming a power upgrade is the answer to a coverage shortfall.
- Site layout should be planned jointly with the hazardous-area classification drawing (Stage 2 item 2) from the start, not as a later retrofit — keeping equipment outside classified zones where possible simplifies certification requirements considerably.

Formal reference: general RF/telecom site-engineering practice (not TETRA-specific) — loss figures are always equipment-specific, sourced from OEM datasheets.
