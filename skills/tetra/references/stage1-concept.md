# Stage 1 — Concept (project inception, pre-tender)

The client has an idea for a rail station/yard/depot radio network, or an oil & gas plant/field radio network, and needs a TETRA feasibility study. The **Consultant** is the primary actor at this stage; no Contractor is engaged yet.

## Sequence

1. Client hires a **Consultant** for feasibility.
2. Consultant runs the **initial survey and feasibility study** — for O&G, this includes an early hazardous-area classification review (which zones exist, even before detailed equipment planning); for rail, an early review of which operational groups need radio coverage (station staff, yard/shunting, maintenance, depot).
3. Consultant **collects requirements from stakeholders** — operations, safety/HSE (critical for O&G hazardous areas), other client departments, the regulator — and identifies which standards apply.
4. Consultant **floats queries to the market** (RFI-style, to TETRA OEMs/system integrators) to get **initial budgetary estimations**.
5. Consultant prepares an **initial high-level proposal**, including **options across different OEMs** (Motorola, Hytera, Airbus, Sepura, etc. — named generically here; never invent specific model data without a source).
6. This proposal, with the **price estimation**, goes into the **main project package** submitted for approval.

## Inputs

- Deployment context (rail station/yard/depot vs O&G plant/field/offshore) and site basics (area, number of buildings/zones, number of expected users/talkgroups — order of magnitude)
- Hazardous-area classification, at least preliminarily, for O&G (any Zone 0/1/2 or Division 1/2 areas expected?)
- Greenfield vs brownfield (existing PMR/analogue radio infrastructure present that needs replacing or interoperating with?)
- Stakeholder requirements: operations, HSE/safety, other client departments, regulatory bodies
- Applicable standards identified for this project/region (national frequency regulator, ATEX/IECEx if hazardous areas apply)
- Country/region (PMR frequency band allocation varies significantly by country/regulator — don't assume a band)
- List of OEMs to approach for market RFI, and what to ask them for (budgetary estimate basis)
- Who the proposal and price estimate go to for approval

## Decisions

Which OEMs to approach; which standards apply; high-level technology direction (TETRA vs a broadband/hybrid alternative, if the client is open to it); which OEM options to present.

## Calculations

Order-of-magnitude/parametric only — approximate site/base-station count from coverage area, approximate user/talkgroup count from headcount and operational structure. Not a detailed link budget or Erlang model yet.

## Deliverables

- Feasibility study report (including preliminary hazardous-area review for O&G)
- Stakeholder requirements register
- Initial high-level proposal, with OEM options
- Budgetary price estimate
- Project approval package

## Roles

- **Consultant** — producer of all deliverables at this stage
- **Client** — requester and final approver of the package
- **OEM/Vendor** — responds to market queries with budgetary data
- **Contractor** — not engaged yet
