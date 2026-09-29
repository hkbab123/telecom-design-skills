# Telecom Design Skills

A family of [Claude Code Skills](https://docs.claude.com/en/docs/claude-code/skills), one per telecom subsystem used on rail and oil & gas projects. Each skill acts as a senior engineer guiding a junior through a design session — not a static reference:

1. Takes project inputs (client specification, route/site data, OEM choice).
2. Walks the engineer through design decisions in the correct order.
3. Checks each decision against the governing standards and the client spec.
4. Helps produce the engineering deliverables for that stage (technical specification, compliance matrix, BOQ basis, etc.).

**Who it's for:** consultants, PMCs, EPC contractors, and vendor engineers working on rail or oil & gas telecom subsystems — GSM-R, TETRA, and PAGA today, with SCADA, CCTV, and fibre backbone planned.

## Status

**Three subsystem skills exist so far, all v0.1:**
- **GSM-R** — the pilot. Its Concept-stage workflow is confirmed practice; the Tender and Engineering sequences are a strong first-pass domain draft, refined against a real cross-border project reference, and open to correction from practicing GSM-R engineers. Also includes a 22-file `references/fundamentals/` layer covering GSM-R's own engineering theory (network architecture and cross-border core placement, EIRENE's <300ms handover requirement, functional addressing, ETCS-bearer data services, RAMS/SIL, and more, each with worked examples) so an engineer doesn't need to search the internet or find a mentor to understand the reasoning behind a decision.
- **TETRA** — built from public ETSI TETRA standards knowledge and general PMR design practice rather than a specific past project. Covers both rail (station/yard/depot voice) and oil & gas (plant/field voice, including ATEX/IECEx hazardous-area equipment requirements) use cases in one skill. Also includes a 26-file `references/fundamentals/` layer — deep-dive engineering explainers (trunking/Erlang theory, RF link budgets, protocol mechanics, hazardous-area technical basis including gas-group/temperature-class certification markings, passive/active outdoor repeaters and cell extenders, antenna/feeder/combiner site hardware, numbering schemes, network synchronization/timing, cybersecurity and IT/OT governance, dispatcher/control-room ergonomics, advanced safety features, and more, each with worked examples) so an engineer using this skill doesn't need to search the internet or find a mentor to understand the reasoning behind a decision, not just the decision sequence itself.

- **PAGA** — built from public IEC 60849/EN 54/ISO 7240 voice-alarm standards knowledge and general PAGA design practice rather than a specific past project. Covers both rail (station/platform public address and evacuation alarm) and oil & gas (plant/offshore Public Address & General Alarm, including Fire & Gas/ESD integration, functional safety for the General Alarm function, and ATEX/IECEx hazardous-area equipment requirements) use cases in one skill. Also includes an 18-file `references/fundamentals/` layer — deep-dive engineering explainers (SPL/STI acoustic theory, constant-voltage line and tap-loading calculations, amplifier redundancy, functional safety/SIL determination for General Alarm, F&G/ESD integration mechanics, fire-survival cabling, hazardous-area equipment certification, offshore/marine considerations, rail-specific design variations, and more, each with worked examples) so an engineer using this skill doesn't need to search the internet or find a mentor to understand the reasoning behind a decision, not just the decision sequence itself.

All three are open to correction from practicing engineers — see [Contributing](#contributing).

## Quick start (Claude Code)

1. Clone this repo.
2. Copy (or symlink) the skill you want into your Claude Code skills folder:

   ```bash
   cp -r skills/gsmr ~/.claude/skills/gsmr
   cp -r skills/tetra ~/.claude/skills/tetra
   cp -r skills/paga ~/.claude/skills/paga
   ```

   For a project-local install instead, copy it into `.claude/skills/<name>` inside your project directory.
3. In Claude Code, trigger it naturally — e.g. "I'm scoping a GSM-R network for a new metro line, walk me through the coverage philosophy decisions," "I need to design a TETRA network for an offshore platform," or "help me design the PAGA evacuation alarm system for a gas plant" — or invoke directly with `/gsmr`, `/tetra`, or `/paga`.

## OEM data disclaimer

No proprietary vendor documentation (Huawei, Nokia, or any other OEM's internal manuals) is included anywhere in this repo. Where a design decision needs an OEM-specific figure this skill doesn't have a public source for, it will say "confirm with OEM" rather than invent one. If you have legitimate access to vendor documentation for your project, supply the relevant figures yourself.

## Roadmap

| Order | Subsystem | Status |
|---|---|---|
| 1 | GSM-R | Pilot — v0.1, project-informed draft |
| 2 | TETRA | v0.1, public-standards-informed draft |
| 3 | PAGA | v0.1, public-standards-informed draft |
| 4 | SCADA | Not started |
| 5 | CCTV | Not started |
| 6 | Fibre backbone | Not started |
| — | FRMCS (GSM-R successor) | Planned second build once the GSM-R pattern is proven |

## Repo structure

```
telecom-design-skills/
├── skills/
│   ├── gsmr/
│   │   ├── SKILL.md            Entry point: intake questions, workflow, design rules
│   │   ├── references/         Stage-by-stage decision sequences and standards list
│   │   └── templates/          Deliverable templates (planned)
│   ├── tetra/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   └── templates/
│   └── paga/
│       ├── SKILL.md
│       ├── references/
│       └── templates/
├── docs/
│   └── design-notes/           Background on how this skill family is designed
└── CONTRIBUTING.md
```

Three subsystems now exist (GSM-R, TETRA, PAGA), each fully self-contained on purpose — see `docs/design-notes/design-philosophy.md` for why the shared `core/` extraction was deliberately deferred until a second subsystem existed to compare against. All three skills share the same stage/role intake shape (Concept → Tender → Engineering, Client/PMC/Consultant/Contractor/Vendor), a design-rules block (no unsourced OEM data, illustrative-figures caveat), and a references/standards.md pattern. Extracting that shared shape into `core/` is a reasonable next step once the skills have had at least one round of real-engineer correction.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Corrections to the Tender and Engineering stage sequences from practicing GSM-R engineers are especially welcome — this is genuinely open to being wrong on ordering or gating details, and it's meant to reflect real practice, not one person's assumption of it.

## License

[MIT](LICENSE) — use, modify, and redistribute freely, with attribution.

## Author

Built by Harish Babry — combining Claude skill development with GSM-R domain expertise.
