# Hazardous-Area Technical Basis

Underpins Stage 2 item 2 (hazardous-area zoning) and every downstream equipment-selection decision it gates — read this for what "ATEX/IECEx certified" actually requires of PAGA equipment specifically, not just as a general label.

## Zone classification is a client-provided input, not a PAGA design decision

Hazardous-area (or "classified area") zoning — Zone 0/1/2 (gas) or Zone 20/21/22 (dust), per **IEC 60079-10** (and the equivalent North American Class/Division system where relevant) — is determined by the facility's process-safety engineering function based on where flammable gas or combustible dust could realistically be present, not by the PAGA designer. PAGA's job is to take this zoning map as a given input (confirmed during Stage 1/Stage 2 intake) and select every piece of equipment placed within a classified zone accordingly — treating the zoning drawing as authoritative and current, and flagging explicitly if it hasn't been issued yet, since equipment selection genuinely cannot proceed without it.

## Which PAGA equipment categories actually need certification

Not every component in a PAGA system needs hazardous-area certification — only what physically sits inside the classified zone:
- **Loudspeakers and horns** mounted in process areas, wellheads, or offshore module spaces — the most common certified item in a PAGA design, since GA coverage typically must extend into the classified zone itself.
- **Junction boxes and cable termination points** within the zone — connection points are a common ignition-risk location if not properly rated.
- **Call stations and local control/indicator panels** if installed within the zone (e.g. a manual call point at a wellhead) — control-room equipment itself is normally outside the classified zone and doesn't need this certification, but any field-mounted operator interface does.
- **Cable glands and cable itself** entering certified enclosures — the gland type must match the enclosure's protection concept, not be selected independently.

Equipment sited in unclassified areas (the control room, the equipment room housing amplifiers and the central controller) doesn't need hazardous-area certification at all — over-specifying certified equipment throughout the whole system wastes cost without a corresponding safety requirement, just as under-specifying it in the zone is a genuine compliance gap.

## Protection concepts — briefly, what the certification marking means

Certified equipment achieves safety through one of several recognised **protection concepts**, each suited to different equipment types:
- **Ex d (flameproof)** — the enclosure is built to contain an internal explosion, preventing it from igniting the surrounding atmosphere; common for junction boxes and some loudspeaker enclosures.
- **Ex i (intrinsic safety)** — the electrical energy in the circuit itself is limited below what could ignite the atmosphere, often used for lower-power field instrumentation and some call-station circuits.
- **Ex e (increased safety)** — relies on enhanced construction and clearance standards to prevent arcs, sparks, or excessive temperature, commonly used for terminal/junction enclosures.

Which concept applies to a given piece of PAGA equipment is a product-design characteristic set by the manufacturer and certifying body, not a choice the PAGA designer makes independently — the design task is matching the zone's requirements to a correctly certified product, not selecting a protection concept in the abstract.

## The certification-attaches-to-specific-product-variant principle

A manufacturer's general product line being "ATEX-rated" doesn't mean every variant, accessory, or configuration of that product carries the certification — certification is issued for a specific model, often a specific hardware revision, sometimes even a specific mounting/accessory combination, documented in that product's certificate and datasheet. This is the same principle already established elsewhere in this skill family (GSM-R and TETRA hazardous-area equipment): never assume a certified base unit's certification extends to an accessory, a different cable gland, or a firmware/hardware revision without confirming the specific certificate covers that exact configuration — this is a genuine, easy-to-miss compliance gap, not a formality.

## Why this matters for design decisions

- Stage 2 item 2 should capture the classified-area zoning drawing as a named, dated input document, not an assumed or informally-described boundary — confirm it exists and is current before equipment selection proceeds.
- Every loudspeaker, junction box, call station, and cable gland placed within a classified zone needs its specific certificate checked against the zone's classification and gas/dust group — not assumed adequate because the product family is generally described as hazardous-area rated.
- Equipment sited outside classified zones shouldn't be over-specified with unnecessary certification, since it adds real cost without a corresponding requirement.

Formal reference: IEC 60079 series (explosive atmospheres — equipment requirements and protection concepts); ATEX Directive 2014/34/EU (EU equipment/certification framework) and the IECEx Scheme (international certification framework) — confirm which regime applies per project jurisdiction.
