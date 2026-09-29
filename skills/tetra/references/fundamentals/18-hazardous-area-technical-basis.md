# Hazardous-Area Technical Basis

What "ATEX/IECEx certified" and "Zone 1" actually mean technically — the concepts behind Stage 2 item 2 and Stage 3 item 14, for O&G deployments.

## Why hazardous areas exist

Anywhere flammable gas, vapour, or combustible dust can be present in a concentration capable of ignition — process plant, wellheads, tank farms, offshore platforms — is a **hazardous area**. Any equipment operating there (including radios) is a potential ignition source (sparking contacts, hot surfaces, electrical arcing) unless specifically designed to prevent that. This is the entire reason ATEX/IECEx certification exists: to certify that a given piece of equipment cannot ignite the surrounding atmosphere under defined conditions.

## Zone classification

Areas are classified by **how often and how long** a flammable atmosphere is likely present:
- **Zone 0** — flammable atmosphere present continuously or for long periods (e.g. inside a tank containing flammable liquid). Highest-risk classification, most restrictive equipment requirements.
- **Zone 1** — flammable atmosphere likely to occur in normal operation (e.g. near a process vent, a point where leaks are plausible during routine operation).
- **Zone 2** — flammable atmosphere not likely in normal operation, and if it occurs, only briefly (e.g. general plant areas near but not immediately at process equipment).
- (North American practice uses a **Division 1/2** system instead, with a broadly similar risk-tiering logic but different technical definitions — confirm which classification system applies per the project's jurisdiction.)

The classification drawing (Stage 2 item 2's key input) is produced by the client's process-safety/HSE engineering function based on the actual plant process and layout — it's an input to the telecom design, not something the telecom engineer determines.

## Protection concepts (how equipment gets certified safe)

Different "Ex" protection types achieve safety through different physical mechanisms — a certified radio will be marked with the specific protection type(s) it uses:
- **Ex d (flameproof enclosure)** — the equipment enclosure is built to contain any internal explosion/arcing without it propagating to the surrounding atmosphere, and to cool escaping gases below ignition temperature. Common for heavier fixed equipment.
- **Ex ia / Ex ib (intrinsic safety)** — the equipment's electrical circuits are designed so they simply cannot release enough energy to ignite the atmosphere, even under fault conditions — this is the protection concept most relevant to handheld radios (Ex ia being the higher-assurance variant, typically required for Zone 0).
- **Ex e (increased safety)** — normal ignition sources (sparking, arcing) are eliminated by design margin and construction quality rather than containment or energy limitation — used for some enclosures and terminals.

Each zone requires equipment certified to an appropriate protection concept and "equipment protection level" (EPL) for that zone — a handheld certified Ex ia for Zone 0 is safe to use in a less demanding Zone 1 or 2, but not vice versa (equipment certified only for Zone 2 must not be used in Zone 0 or 1).

## Reading a certification marking — gas group and temperature class

A certified radio's rating plate carries more than just the protection concept (Ex ia, Ex d, etc.) — it also states a **gas group** and a **temperature class**, both of which must match the actual hazard present, not just the protection concept in isolation:
- **Gas group** (e.g. IIA, IIB, IIC for surface industries — IIC being the most demanding, covering the most easily ignitable gases such as hydrogen) — confirms the equipment is certified for the specific gas/vapour actually present on site, not gas-hazardous-areas in general. A device certified only IIA is not automatically safe where the process handles a IIC-group gas.
- **Temperature class** (T1 through T6, e.g. T4 meaning the equipment's maximum surface temperature stays below 135°C) — confirms the equipment's hottest surface stays below the ignition temperature of the specific gas/vapour present, since different flammable substances ignite at different surface temperatures.

A radio marked, for example, "Ex ia IIC T4" is certified intrinsically-safe, for the most demanding gas group, with a maximum surface temperature safely below 135°C — but the specific combination needed on a given project depends entirely on the actual gas(es) present and their ignition temperature, confirmed from the client's process-safety documentation, not assumed from the zone number alone. Two sites both classified Zone 1 can still require different gas-group/temperature-class combinations if they handle different substances.

## Installation practice, independent of equipment certification

A correctly certified device can still become non-compliant through incorrect installation: cable glands must themselves be certified and correctly torqued/sealed, junction boxes and enclosures need matching Ex ratings, and equipotential bonding/earthing must follow the applicable installation standard (IEC 60079-14). This is why Stage 3 item 14 (hazardous-area installation design) is listed as **independent** from equipment certification (item 9) — both need to be right, and installation errors are a common real-world non-compliance point even when the equipment itself is properly certified.

## Why this matters for design decisions

- The classification drawing is a hard input, not a telecom design output — Stage 2 item 2 correctly treats obtaining it as the first step, not something to defer.
- Equipment selection (Stage 2 item 9) must match the specific zone and protection-level requirement per location — a single "hazardous-area-rated" spec line isn't sufficient; different zones on the same site may need different certified variants.
- Equipment selection must also match the specific gas group and temperature class actually present (from the client's process-safety documentation), not just the zone number — confirm this explicitly rather than assuming a generic "Ex-rated" spec covers whatever gas the site actually handles.
- Installation verification (Stage 3 item 18's FAT/SAT) should explicitly check installed configuration against the certificate, not just confirm the equipment itself carries a certificate — a certified device installed with an uncertified cable gland, or modified after certification, invalidates the certification in practice even though the nameplate still says "certified."

Formal reference: IEC 60079 series (equipment: -0 general requirements plus part-specific standards per protection type; installation: -14; zoning: -10); ATEX Directive 2014/34/EU (EU equipment-placement regime); IECEx Scheme (broader international certification scheme).
