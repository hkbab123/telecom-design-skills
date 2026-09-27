# Design philosophy

Notes on why this skill family is built the way it is, for anyone extending it.

## Why "senior engineer guiding a junior," not a reference lookup

A telecom subsystem design session is a sequence of dependent decisions, not a set of independent questions. Coverage philosophy constrains cell planning, which constrains the link budget, which constrains equipment dimensioning. A skill that just answers isolated questions ("what's the EIRENE handover target?") is a worse use of an LLM than one that walks the sequence in order and checks each decision against what was decided earlier. That's the shape every subsystem skill in this repo should take.

## Why stage + role gate everything

The same subsystem looks completely different depending on where the project is in its lifecycle (Concept / Tender / Engineering) and who the user represents (Client, PMC, Consultant, Contractor, Vendor). A Client at Tender stage is usually reviewing a document someone else drafted; a Contractor at the same stage is producing a bid. Asking both questions up front, before giving any domain guidance, is what makes the rest of the interaction useful rather than generic.

## Why the OEM-sourcing rule is non-negotiable

Any AI-assisted design tool that invents plausible-sounding vendor figures (capacity numbers, model specs) is actively dangerous in a safety-relevant domain like railway radio. The rule — never state an OEM-specific parameter without a source, say "confirm with OEM" instead — exists to keep the skill honest about the boundary between "general engineering knowledge" and "this specific vendor's actual product," and it's also why no licensed OEM documentation is or will be included in this public repo.

## Why "shared core, thin subsystem skills" waits until the second subsystem

It's tempting to build a shared `core/` from day one. In practice, the right shared abstraction only becomes visible once there's a second real subsystem to compare against — building it against one data point (GSM-R alone) risks baking in GSM-R-specific assumptions as if they were general. The plan is deliberately: prove the pattern once, fully, then extract what's actually shared when TETRA (or another subsystem) is built.
