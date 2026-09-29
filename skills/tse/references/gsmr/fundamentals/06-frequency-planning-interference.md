# Frequency Planning & Interference

The technical basis behind GSM-R frequency/channel planning — read this when the question is "how does reuse and interference management actually work for R-GSM 900."

## Channel raster and R-GSM 900

GSM channels sit on a **200 kHz raster** within the allocated band. GSM-R's R-GSM 900 allocation is narrower than a typical public operator's full spectrum holding — a genuinely scarce resource, which makes efficient frequency planning more consequential for GSM-R than for a public network with abundant spectrum.

## Frequency reuse along a linear corridor

Unlike an area-coverage network's two-dimensional reuse pattern, a rail-corridor network's reuse planning is largely **one-dimensional** — frequencies are assigned to cells along the chain such that cells close enough together to interfere don't share the same frequency, but cells further apart along the line (or on parallel/non-adjacent lines) can reuse it. This constrained geometry is actually somewhat simpler to reason about than general two-dimensional cellular reuse, but the limited overall spectrum (see above) still makes the reuse pattern a tight optimisation problem, especially on lines with many closely-spaced stations/junctions needing smaller cells.

## Co-channel and adjacent-channel interference

- **Co-channel interference** — two cells on the same frequency close enough together that coverage overlaps degrade calls in the overlap zone — managed by reuse distance along the corridor and by antenna directionality (most trackside BTS antennas are already directional, aimed along the corridor, which naturally helps limit interference to cells behind/beside rather than just ahead).
- **Adjacent-channel interference** — imperfect receiver filtering picking up energy from a neighbouring channel — managed by guard-band planning and equipment filter specifications, same principle as general cellular practice.

## Interference from public GSM/E-GSM networks

Because R-GSM 900 sits adjacent to (and is an extension of) the standard E-GSM 900 band used by public mobile operators in many countries, interference coordination with the national regulator and with public operators using adjacent spectrum is a real, recurring coordination task — not a one-time licensing formality. This is more pronounced for GSM-R than for TETRA (which typically sits in a separate PMR band with less direct adjacency to high-traffic public cellular spectrum) and is a specific reason frequency-plan review needs to be revisited whenever a public operator's spectrum usage or network changes nearby.

## Cross-border frequency coordination

For cross-border lines, each country's national regulator independently allocates R-GSM 900 channels, and coordination is needed at the border to avoid one country's cell plan interfering with the other's — a genuinely bilateral regulatory/engineering coordination exercise, distinct from (though related to) the independent-core-per-country architecture decision covered in the network-architecture fundamentals file. Frequency coordination and core architecture are both consequences of cross-border operation but are separate technical/regulatory processes.

## Why this matters for design decisions

- R-GSM 900's limited bandwidth makes frequency plan efficiency a genuine cost/feasibility constraint, not just an interference-avoidance exercise — over-conservative reuse spacing can make a design infeasible within the available spectrum.
- Coordination with adjacent public-operator spectrum usage should be treated as an ongoing relationship with the regulator, not a one-off tender-stage approval — worth flagging in the regulatory approvals item of the Stage 2 sequence with this ongoing-coordination framing.
- Cross-border frequency coordination is a distinct deliverable from the cross-border core-interworking design — both need to appear in a cross-border project's technical specification, not conflated into one "cross-border" line item.

Formal reference: 3GPP GSM band-plan specifications (R-GSM 900 definition) plus each national telecom regulator's specific allocation and licensing conditions — always project- and country-specific, doubly so for cross-border projects.
