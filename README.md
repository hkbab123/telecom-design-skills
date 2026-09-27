# Telecom Design Skills

A family of [Claude Code Skills](https://docs.claude.com/en/docs/claude-code/skills), one per telecom subsystem used on rail and oil & gas projects. Each skill acts as a senior engineer guiding a junior through a design session — not a static reference:

1. Takes project inputs (client specification, route/site data, OEM choice).
2. Walks the engineer through design decisions in the correct order.
3. Checks each decision against the governing standards and the client spec.
4. Helps produce the engineering deliverables for that stage (technical specification, compliance matrix, BOQ basis, etc.).

**Who it's for:** consultants, PMCs, EPC contractors, and vendor engineers working on rail or oil & gas telecom subsystems — GSM-R today, with TETRA, PAGA, SCADA, CCTV, and fibre backbone planned.

## Status

**GSM-R is the pilot subsystem (v0.1).** Its Concept-stage workflow is confirmed practice; the Tender and Engineering sequences are a strong first-pass domain draft, refined against a real cross-border project reference, and open to correction from practicing GSM-R engineers — see [Contributing](#contributing). Other subsystems haven't been started yet.

## Quick start (Claude Code)

1. Clone this repo.
2. Copy (or symlink) the skill you want into your Claude Code skills folder:

   ```bash
   cp -r skills/gsmr ~/.claude/skills/gsmr
   ```

   For a project-local install instead, copy it into `.claude/skills/gsmr` inside your project directory.
3. In Claude Code, trigger it naturally — e.g. "I'm scoping a GSM-R network for a new metro line, walk me through the coverage philosophy decisions" — or invoke it directly with `/gsmr`.

## OEM data disclaimer

No proprietary vendor documentation (Huawei, Nokia, or any other OEM's internal manuals) is included anywhere in this repo. Where a design decision needs an OEM-specific figure this skill doesn't have a public source for, it will say "confirm with OEM" rather than invent one. If you have legitimate access to vendor documentation for your project, supply the relevant figures yourself.

## Roadmap

| Order | Subsystem | Status |
|---|---|---|
| 1 | GSM-R | Pilot — v0.1 |
| 2 | TETRA | Not started |
| 3 | PAGA | Not started |
| 4 | SCADA | Not started |
| 5 | CCTV | Not started |
| 6 | Fibre backbone | Not started |
| — | FRMCS (GSM-R successor) | Planned second build once the GSM-R pattern is proven |

## Repo structure

```
telecom-design-skills/
├── skills/
│   └── gsmr/
│       ├── SKILL.md            Entry point: intake questions, workflow, design rules
│       ├── references/         Stage-by-stage decision sequences and standards list
│       └── templates/          Deliverable templates (planned)
├── docs/
│   └── design-notes/           Background on how this skill family is designed
└── CONTRIBUTING.md
```

A shared `core/` (intake process, document templates, compliance-matrix format, review checklist) will be extracted once a second subsystem skill is built, so the workflow logic isn't duplicated across subsystems.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Corrections to the Tender and Engineering stage sequences from practicing GSM-R engineers are especially welcome — this is genuinely open to being wrong on ordering or gating details, and it's meant to reflect real practice, not one person's assumption of it.

## License

[MIT](LICENSE) — use, modify, and redistribute freely, with attribution.

## Author

Built by Harish Babry — combining Claude skill development with GSM-R domain expertise.
