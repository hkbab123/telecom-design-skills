# Fire-Survival Cabling and Segregation

Underpins Stage 2 item 11 (cabling) and Stage 3 item 10 (cabling detailed design) — read this for why GA cabling has requirements standard electrical/data cabling doesn't.

## Why GA circuits specifically need fire-survival cable

A standard cable's insulation fails within minutes of direct fire exposure, opening the circuit. For most systems that's an acceptable failure mode — but for a GA circuit, the moments during an actual fire are precisely when the evacuation instruction is most needed, meaning the cable carrying that instruction needs to keep functioning *through* fire exposure for a defined period, not just up until the fire reaches it. **Fire-survival cable** (sometimes called fire-resistant or circuit-integrity cable, with specific product families like FP-rated cable in some markets, or equivalents rated to the applicable national standard) is engineered and tested to maintain electrical circuit integrity for a stated duration — commonly expressed in minutes (e.g. maintaining function for a defined period under a standardised fire-exposure test) — under direct flame exposure, unlike standard cable.

## What "fire-survival rated" actually means, mechanically

The rating comes from a standardised fire-endurance test (the specific test and duration standard varies by jurisdiction — confirm which national/regional standard applies) where a sample of the cable is subjected to direct flame at a controlled temperature for a set period while energised, and the circuit must continue to function (not just avoid catching fire itself) throughout. This is a fundamentally different and stricter requirement than a cable simply being "fire-retardant" (resists spreading flame along its own length, a property of general low-smoke/fire-retardant cable used throughout most buildings) — fire-retardant and fire-survival are not the same property, and specifying one when the other is actually required is a genuine compliance gap worth catching explicitly.

## Segregation — why fire-survival cable alone isn't the whole requirement

Even a fire-survival-rated GA cable can be compromised if it's bundled together with non-fire-rated cabling or power cabling in a way that a fire or fault in the adjacent cable damages the GA cable's mechanical support or creates an electrical fault by proximity. Applicable fire codes and cabling standards typically require **physical segregation** — GA cabling routed in its own dedicated containment (separate cable tray, conduit, or a defined minimum separation distance) from power cabling and from non-fire-rated data/PA-only cabling — as a complementary requirement to the cable's own fire rating, not a substitute for it.

## Where this applies: which circuits, not the whole system

Fire-survival cabling and segregation requirements apply specifically to circuits carrying the **General Alarm** function — the loudspeaker lines, the F&G/ESD trigger interface (fundamentals file 09), and the power feed keeping GA operational. PA-only circuits (background paging in a low-risk area, for instance) don't automatically carry the same fire-survival cabling requirement — another place where the explicit PA/GA zone tagging established in fundamentals file 01 determines what cabling standard actually applies, avoiding the cost (and false sense of consistency) of over-specifying fire-survival cable everywhere, or the compliance gap of under-specifying it where GA actually needs it.

## Why this matters for design decisions

- Stage 2 item 11 should specify fire-survival cable (with a stated duration rating against the applicable national standard) explicitly for every GA-tagged circuit, distinct from ordinary fire-retardant cable used elsewhere in the project — confirm the two properties aren't being conflated in the specification.
- Segregation requirements (dedicated containment, minimum separation from power/non-fire-rated cabling) should be captured as an explicit cable-routing design rule in Stage 3 item 10, not left to be resolved ad hoc during installation.
- Cable specification should be cross-checked against the PA/GA zone tagging (fundamentals file 01) so fire-survival requirements are applied precisely where GA circuits actually run, not uniformly (wasteful) or inconsistently (a compliance gap).

Formal reference: national/local fire and cabling codes set the actual fire-survival duration rating and segregation requirement (jurisdiction-specific — confirm per project); EN 54-16 references the overall system-reliability expectation this cabling requirement supports.
