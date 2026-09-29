# Contributing

This project welcomes corrections and additions from practicing telecom engineers on rail and oil & gas projects — that's the point of publishing it.

## Most valuable right now

GSM-R's Tender-stage (18-point) and Engineering-stage (20-step) decision sequences in `skills/tse/references/gsmr/` are a domain-expert first draft. If you work on GSM-R projects, the most useful contribution is:

- Correcting the **order** of any decision or step that doesn't match how it actually gates the ones around it.
- Flagging anything that's **missing** (e.g. a specific EIRENE clause you always check, an environmental/EMC consideration, spares/O&M provisioning).
- Flagging anything **misplaced** — e.g. something drafted as a Tender-stage decision that's really an Engineering-stage concern, or vice versa.
- Sharpening the **document-gating** notes in `stage3-engineering.md` — which deliverables actually have to be signed off before which others can proceed, on real projects you've worked.

## How to propose a change

1. Open an issue describing the correction, with your reasoning (a line or two on *why* is more useful than the correction alone — it helps evaluate edge cases).
2. Or open a pull request directly against the relevant file in `skills/tse/references/gsmr/`.

## Adding a new subsystem

All subsystems (GSM-R, TETRA, PAGA today; SCADA, CCTV, fibre backbone, PABX, VSAT, and others planned) live inside the single `skills/tse/` skill. Adding a new one follows the same pattern each time: a `skills/tse/references/<subsystem>/GUIDE.md` entry point (subsystem-specific design rules, stage/role intake mechanics) plus stage-specific decision sequences and a fundamentals layer, written the same way as `skills/tse/references/gsmr/`. If you want to lead one of these, open an issue first so effort isn't duplicated.

## What won't be accepted

- Any content sourced from licensed/proprietary OEM documentation (vendor manuals, confidential datasheets). Public datasheets and general engineering know-how are fine; anything under an NDA or vendor confidentiality terms is not, even if you have legitimate access to it yourself.
- Client-specific data from a real, identifiable project. Anonymised, generalised patterns are welcome; a client's actual site list, pricing, or spec text is not.
