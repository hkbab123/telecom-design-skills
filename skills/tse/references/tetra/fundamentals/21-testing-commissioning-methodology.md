# Testing & Commissioning Methodology

How coverage/functionality testing is actually run and interpreted — the method behind Stage 2 item 18 and Stage 3 item 18, read when the question is "how do I actually run and interpret a coverage/drive test," not just "verify against the target."

## Coverage verification (drive/walk testing)

A field measurement campaign that samples actual received signal (and, for a fuller test, actual call-success/voice-quality outcomes) at many locations across the intended coverage area, then compares the result against the predicted coverage (from the RF planning tool output referenced in Stage 3 item 6) and the target from Stage 2 item 1.

- **Drive testing** — for vehicle-accessible areas (rail yards, plant roads), a test terminal and measurement equipment mounted in a vehicle logs signal strength/quality continuously along a driven route, typically GPS-tagged so results map directly onto the coverage prediction.
- **Walk testing** — for areas a vehicle can't reach (inside plant structures, tight yard areas, platforms), the same principle on foot, at a lower coverage-sampling rate per unit time but necessary for exactly the "hardest, most safety-relevant" in-building/in-plant coverage areas flagged in the propagation fundamentals file (04).

## What the test actually measures and how to interpret it

Raw output is typically received signal strength/quality at each sampled point, statistically summarised as **location probability** (what percentage of sampled locations met the signal threshold) — matching the same metric the original coverage target (Stage 2 item 1) should have been expressed in, so the two are directly comparable. A result that falls short of target in a specific area points back to the propagation model/assumptions used for that area (fundamentals file 04) — the fix is usually a design adjustment (additional site, antenna change, repeater) in that specific location, not a network-wide redesign.

## FAT (Factory Acceptance Test) vs SAT (Site Acceptance Test)

- **FAT** — equipment tested at the manufacturer's/integrator's facility before shipment, verifying it meets specification in a controlled environment (functional tests, not real-world coverage — coverage can't be tested until equipment is actually installed on site).
- **SAT** — the same and additional tests repeated after installation on the actual site, including the field coverage verification above, functional testing of the actually-installed configuration (talkgroups, priority/pre-emption behaviour, interfaces), and — for O&G hazardous-area equipment — a specific check that the as-installed configuration matches the certified configuration (fundamentals file 18's installation-practice point), since installation errors are a real, common compliance gap even for equipment that passed FAT.

## Acceptance criteria should be objective and pre-agreed

Stage 2 item 17's "testing/acceptance criteria" should specify, in advance, exactly what SAT must demonstrate to be accepted — the location-probability coverage target, specific functional tests (a defined list of features/talkgroups/priority scenarios to verify), and the hazardous-area certification-match check — so that acceptance isn't a subjective judgment call made after installation, but a pre-agreed, objectively verifiable pass/fail test.

## Coordinating with O&G site access requirements

Field testing (walk/drive testing, and SAT more broadly) inside an O&G plant needs to be coordinated with the site's permit-to-work system, and personnel entering classified hazardous zones for testing need the same qualification/certification awareness as anyone else entering those zones — this is an operational planning requirement for the test campaign itself, not just a design consideration.

## Why this matters for design decisions

- Coverage verification methodology (this file) is what actually validates or invalidates every propagation-model assumption made earlier (fundamentals file 04) — treat a coverage shortfall found in testing as evidence to correct the design assumption, not just a local patch.
- Pre-agreeing objective SAT acceptance criteria (Stage 2 item 17) avoids disputes at commissioning — this deserves more concrete detail in the technical specification than a generic "field measurement campaign" statement.
- Hazardous-area installation verification at SAT (checking as-installed vs certified configuration) is a distinct, easy-to-skip check that should be explicit in the SAT procedure, not assumed to be covered by "the equipment has a certificate."

Formal reference: no TETRA-specific standard governs test methodology — general telecom RF coverage testing and acceptance-testing practice, applied to a TETRA deployment.
