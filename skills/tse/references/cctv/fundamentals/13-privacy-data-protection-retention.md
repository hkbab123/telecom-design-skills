# Privacy, Data Protection, and Retention

Recorded CCTV footage is personal data under most data-protection regimes (GDPR and its equivalents elsewhere) whenever it can identify an individual — which most CCTV footage can. This has real design implications, not just a legal-compliance checkbox:

**Retention period** must be justified against a stated purpose, not set indefinitely "just in case" — most data-protection regimes require retention to be proportionate and documented. A typical pattern is a short default retention (e.g. 30 days) with a defined process for extending retention on specific footage when it's needed as evidence for an ongoing investigation (at which point it's handled outside the routine retention cycle).

**Access control and audit trail.** Who can view live footage, who can export recorded footage, and who can be shown that footage (e.g. a data-subject-access request) all need to be logged and restricted by role — this is both a data-protection requirement and (per `fundamentals/12-cybersecurity-vendor-compliance.md`) an evidentiary-integrity requirement. An audit trail of every export/view action protects both the individual's privacy rights and the organisation if footage is later relied on as evidence.

**Privacy masking.** Where a camera's field of view unavoidably captures an area outside its intended purpose (e.g. a public street visible from a perimeter camera, or a neighbouring private property), some VMS platforms support digital privacy-masking of that zone in both live view and recording — worth considering explicitly at the coverage-design stage rather than accepting an over-broad field of view by default.

**Signage and notification.** Most regimes require visible signage informing the public that CCTV is in operation — a physical-design/procurement item easy to treat as trivial but genuinely required for compliance in most jurisdictions.

**Why this matters for design decisions:** data-protection compliance shapes retention-period sizing (which directly drives the storage calculation, `fundamentals/04-bandwidth-storage-calculations.md`) and VMS access-control configuration — it's not a separate legal workstream bolted on afterward, it's an input to the technical spec.

**Formal reference:** GDPR (EU) or the applicable national/regional data-protection regime — always confirm which applies for the specific jurisdiction; this skill does not assume any one regime applies by default.
