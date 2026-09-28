# Testing, Commissioning, and Verification Methodology

Underpins Stage 3 items 17-18 (testing and commissioning) — read this for what actually needs to be verified before a PAGA system is handed over, and why each test type exists.

## Why PAGA commissioning is more than "does sound come out"

A PAGA system can appear to work — announcements audible, loudspeakers producing sound — while still failing the requirements that actually matter for its safety function: intelligibility might be below target in a specific reverberant zone, the GA priority-override might not actually pre-empt an active PA announcement, a supervised line fault might not actually report to the controller, or the F&G/ESD automatic trigger might not fire within the required activation time. Commissioning needs to verify each of these specifically, not just confirm general audibility.

## The core test categories

- **Acoustic verification (SPL and STI/CIS)** — measuring actual delivered sound pressure level and intelligibility in each zone against the targets set in fundamentals file 02, using real ambient-noise conditions where practical (or a documented worst-case assumption where not) — not just confirming the system is audible in a quiet, empty space during a daytime test.
- **Supervision fault-injection testing** — deliberately introducing an open circuit, short circuit, and (where the system supports it) a degraded connection on a supervised line, and confirming the controller correctly reports each specific fault type (fundamentals file 06) — testing that the alarm *would* trigger isn't the same as testing that a *fault* is correctly detected and reported.
- **Redundancy/failover testing** — deliberately failing a primary amplifier (or controller, depending on the architecture) and confirming the standby takes over within the expected switchover time (fundamentals file 05) — not just confirming redundant hardware exists.
- **Priority/override testing** — triggering a GA event during an active PA announcement and confirming GA takes over immediately and completely (fundamentals file 08) — a test easy to skip because it requires deliberately creating a conflict scenario, but one of the more likely-to-be-wrong behaviours if never explicitly tested.
- **F&G/ESD automatic-activation testing** — triggering the actual upstream F&G/ESD interface (or a documented simulation of it, where triggering the live safety system isn't practical) and confirming the correct GA response fires within the specified activation time (fundamentals file 09) — jointly verified with the F&G/ESD system's own commissioning team, since this test spans both systems.
- **Battery autonomy verification** — either a full discharge test or a calculation-based verification against the actual as-built load figures (fundamentals file 10), confirming the delivered system meets the autonomy duration the design targeted, not just the theoretical figure from the design calculation.
- **Functional-safety verification (where GA is SIL-rated)** — a distinct verification package (fundamentals file 07) confirming the as-built system's PFD, diagnostic coverage, and proof-test interval meet the determined SIL target — typically requires its own dedicated verification activity separate from the general commissioning test list above, often involving the client's functional-safety assessor.

## Document gating before commissioning starts

Several of these tests can't happen — or can't be meaningfully interpreted — until specific documents exist: acoustic verification needs the ambient-noise survey and acoustic model it's being checked against; the F&G/ESD test needs the cause-and-effect matrix and ICD signed off; the SIL verification needs the formal SIL determination and its associated proof-test/diagnostic-coverage targets defined. Confirm each prerequisite document exists and is current before scheduling the corresponding test, rather than discovering the gap mid-commissioning.

## Why this matters for design decisions

- Stage 3 item 17's test plan should explicitly list each of these test categories by name with its own pass/fail criteria, rather than a single generic "system test" — a system that's audible but fails intelligibility, supervision, or priority testing is not actually complete.
- Priority/override and supervision fault-injection testing are the two categories most likely to be skipped under commissioning time pressure precisely because the system "sounds fine" without them — flag these explicitly as non-negotiable line items.
- Where GA is SIL-rated, the functional-safety verification should be scheduled and resourced as its own distinct activity, not assumed covered by general commissioning sign-off.

Formal reference: IEC 60849 and EN 54-16 set the underlying performance requirements being verified; IEC 61508/61511 govern the specific verification methodology where GA is SIL-rated; national/local fire code and the project's own commissioning specification govern the acceptance test procedure format.
