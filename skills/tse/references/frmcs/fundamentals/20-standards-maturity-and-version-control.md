# Standards Maturity and Version Control

**Technical basis for Rule 4:** pin the standards baseline.

## Why it matters

FRMCS rests on specification sets from several bodies that release on different schedules. A design that names "FRMCS" without a baseline cannot be tendered, tested or defended: suppliers will interpret different releases, interoperability will fail on details, and later changes become disputes.

## The moving parts

- **UIC FRMCS specifications** (URS, FRS, SRS and supporting documents) — released as numbered versions.
- **3GPP releases** — mission-critical services and 5G features arrive per release; railway-specific features are added over several releases.
- **ETSI documents** — system-level and test specifications that follow the UIC and 3GPP work.
- **ERA / EU regulation** — which versions are mandatory for interoperability, and the transition rules.
- **Signalling specifications** — ETCS baselines and their communication requirements.
- **CEPT/regulatory decisions** — spectrum conditions.

## Defining the baseline

In the Tender spec, list for each family: document, version/release, date checked, status (mandatory, recommended, draft), and the person who checked it. For items still in draft, decide whether the design depends on them and what the fallback is.

## Control after award

1. A **baseline register** held by the contractor and the client.
2. A **change procedure** when a baseline moves: impact assessment on RF, core, on-board and interfaces; cost and programme effect; test impact.
3. **Backward compatibility policy** — how long older equipment must interoperate with newer releases.
4. **Release management** — software update strategy across multi-vendor trackside and fleet equipment; synchronised release windows; rollback.

## Using this skill's content

Specification numbers, band allocations and release statements in this folder are pointers written from general knowledge. Before a figure or requirement goes into a deliverable, confirm it against the source and record the version in the baseline register.

## Common mistakes

- "FRMCS-compliant" with no version.
- Mixing equipment built to different releases without an interoperability plan.
- Letting suppliers define the baseline.
- No owner for tracking changes after contract award.
