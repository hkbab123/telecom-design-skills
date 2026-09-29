# Telecom Design Skills

A single [Claude Code Skill](https://docs.claude.com/en/docs/claude-code/skills) — **Telecom System Engineering (TSE)** — covering every telecom/instrumentation subsystem used on rail and oil & gas projects. It acts as a senior engineer guiding a junior through a design session — not a static reference:

1. Takes project inputs (client specification, route/site data, OEM choice).
2. Establishes which subsystem is in play, then walks the engineer through that subsystem's design decisions in the correct order.
3. Checks each decision against the governing standards and the client spec.
4. Helps produce the engineering deliverables for that stage (technical specification, compliance matrix, BOQ basis, etc.).

**Who it's for:** consultants, PMCs, EPC contractors, and vendor engineers working on rail or oil & gas telecom subsystems — GSM-R, TETRA, and PAGA today, with SCADA, CCTV, fibre backbone, and more being added to the same skill over time.

## Status

**One skill (`tse`), three subsystems built so far, all v0.1:**
- **GSM-R** — the pilot. Its Concept-stage workflow is confirmed practice; the Tender and Engineering sequences are a strong first-pass domain draft, refined against a real cross-border project reference, and open to correction from practicing GSM-R engineers. Also includes a 22-file fundamentals layer covering GSM-R's own engineering theory (network architecture and cross-border core placement, EIRENE's <300ms handover requirement, functional addressing, ETCS-bearer data services, RAMS/SIL, and more, each with worked examples) so an engineer doesn't need to search the internet or find a mentor to understand the reasoning behind a decision.
- **TETRA** — built from public ETSI TETRA standards knowledge and general PMR design practice rather than a specific past project. Covers both rail (station/yard/depot voice) and oil & gas (plant/field voice, including ATEX/IECEx hazardous-area equipment requirements) use cases. Also includes a 26-file fundamentals layer — deep-dive engineering explainers (trunking/Erlang theory, RF link budgets, protocol mechanics, hazardous-area technical basis including gas-group/temperature-class certification markings, passive/active outdoor repeaters and cell extenders, antenna/feeder/combiner site hardware, numbering schemes, network synchronization/timing, cybersecurity and IT/OT governance, dispatcher/control-room ergonomics, advanced safety features, and more, each with worked examples) so an engineer using this skill doesn't need to search the internet or find a mentor to understand the reasoning behind a decision, not just the decision sequence itself.
- **PAGA** — built from public IEC 60849/EN 54/ISO 7240 voice-alarm standards knowledge and general PAGA design practice rather than a specific past project. Covers both rail (station/platform public address and evacuation alarm) and oil & gas (plant/offshore Public Address & General Alarm, including Fire & Gas/ESD integration, functional safety for the General Alarm function, and ATEX/IECEx hazardous-area equipment requirements) use cases. Also includes an 18-file fundamentals layer — deep-dive engineering explainers (SPL/STI acoustic theory, constant-voltage line and tap-loading calculations, amplifier redundancy, functional safety/SIL determination for General Alarm, F&G/ESD integration mechanics, fire-survival cabling, hazardous-area equipment certification, offshore/marine considerations, rail-specific design variations, and more, each with worked examples) so an engineer using this skill doesn't need to search the internet or find a mentor to understand the reasoning behind a decision, not just the decision sequence itself.

All three are open to correction from practicing engineers — see [Contributing](#contributing).

**Restructured 29-Sep-26** from three separate published skills (`gsmr`, `tetra`, `paga`) into this single `tse` umbrella skill, so the whole subsystem pool (built and planned) lives under one install rather than one skill per subsystem. Content is unchanged — only the entry-point mechanics moved.

## Quick start (Claude Code)

1. Clone this repo.
2. Copy (or symlink) the skill into your Claude Code skills folder:

   ```bash
   cp -r skills/tse ~/.claude/skills/tse
   ```

   For a project-local install instead, copy it into `.claude/skills/tse` inside your project directory.
3. In Claude Code, trigger it naturally — e.g. "I'm scoping a GSM-R network for a new metro line, walk me through the coverage philosophy decisions," "I need to design a TETRA network for an offshore platform," or "help me design the PAGA evacuation alarm system for a gas plant" — or invoke directly with `/tse`. It will ask which subsystem you mean if it isn't already clear.

## OEM data disclaimer

No proprietary vendor documentation (Huawei, Nokia, or any other OEM's internal manuals) is included anywhere in this repo. Where a design decision needs an OEM-specific figure this skill doesn't have a public source for, it will say "confirm with OEM" rather than invent one. If you have legitimate access to vendor documentation for your project, supply the relevant figures yourself.

## Roadmap

Subsystems already built (full stage sequences + fundamentals layer): **GSM-R, TETRA, PAGA**.

Subsystems in the pool, not yet built — added one at a time as research data comes in:

| Subsystem | Status |
|---|---|
| SCADA | Not started |
| CCTV | Not started |
| Fibre backbone / transmission (SDH/DWDM/OTN) | Not started |
| PABX | Not started |
| VSAT (incl. hub/DAMA-TDMA) | Not started |
| Master clock / timing systems | Not started |
| Security & access control (perimeter/IDS/ACS) | Not started |
| Passenger information systems (PIDS/VEID/Passenger Help Points) | Not started |
| Marine / aeronautical / HF / UHF radio | Not started |
| Station management systems | Not started |
| Platform screen doors | Not started |
| FRMCS (GSM-R successor) | Planned second build once the GSM-R pattern is proven |

## Repo structure

```
telecom-design-skills/
├── skills/
│   └── tse/
│       ├── SKILL.md                  Entry point: subsystem selection, shared design rules, intake questions
│       ├── references/
│       │   ├── gsmr/
│       │   │   ├── GUIDE.md          GSM-R subsystem guide (subsystem-specific rules, workflow)
│       │   │   ├── stage1-concept.md, stage2-tender.md, stage3-engineering.md, standards.md
│       │   │   └── fundamentals/     22 files, deep-dive engineering theory
│       │   ├── tetra/                same shape, 26 fundamentals files
│       │   └── paga/                 same shape, 18 fundamentals files
│       └── templates/
│           ├── gsmr/, tetra/, paga/  Deliverable templates (planned)
├── docs/
│   └── design-notes/                 Background on how this skill is designed
└── CONTRIBUTING.md
```

Three subsystems now exist (GSM-R, TETRA, PAGA) inside the single `tse` skill, each self-contained under its own `references/<subsystem>/` folder — see `docs/design-notes/design-philosophy.md` for the earlier per-skill design reasoning, most of which still applies at the subsystem-folder level. All three subsystems share the same stage/role intake shape (Concept → Tender → Engineering, Client/PMC/Consultant/Contractor/Vendor), a design-rules block (no unsourced OEM data, illustrative-figures caveat — now partly hoisted into the umbrella `SKILL.md`), and a `standards.md` pattern.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Corrections to the Tender and Engineering stage sequences from practicing engineers are especially welcome — this is genuinely open to being wrong on ordering or gating details, and it's meant to reflect real practice, not one person's assumption of it.

## License

[MIT](LICENSE) — use, modify, and redistribute freely, with attribution.

## Author

Built by Harish Babry — combining Claude skill development with GSM-R domain expertise.
