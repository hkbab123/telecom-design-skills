# Hazardous-Area Camera Certification

Same regime as TETRA/PAGA/SCADA's O&G hazardous-area discipline, applied to cameras: any camera, housing, cable gland, or junction box located in a classified zone (where flammable gas/vapour or combustible dust may be present) needs equipment certified for that specific zone and gas-group/temperature-class — an off-the-shelf IP camera is not automatically suitable just because it's "rated for outdoor use."

**Ex-rated (explosion-proof) camera housings** are purpose-built enclosures that either contain any potential ignition source (flameproof, "Ex d") or are designed to prevent an explosive atmosphere reaching the ignition source at all (e.g. purged/pressurised, "Ex p"). The certification (ATEX in the EU, IECEx internationally, or the relevant national scheme) must match the zone classification (Zone 0/1/2 for gas, Zone 20/21/22 for dust) and the gas group/temperature class of the specific hazard present.

**What this constrains in practice:** camera selection (fundamentals/02), cable and gland selection, mounting-bracket material, and even lens/window material can all be affected once a camera sits in a classified zone — this is why hazardous-area zoning has to be confirmed before equipment dimensioning (Stage 2 item 9), not discovered during procurement.

**Why this matters for design decisions:** skipping this check is the single most expensive mistake a CCTV design can make on an O&G project — a non-certified camera installed in a classified zone is a safety and regulatory non-compliance, not just a spec deviation, and retrofitting certified equipment after installation costs far more than specifying it correctly up front.

**Formal reference:** IEC 60079 series, ATEX Directive 2014/34/EU, IECEx Scheme certification documents (confirm the specific zone/gas-group/temperature-class requirement per site — never assume a generic rating is sufficient).
