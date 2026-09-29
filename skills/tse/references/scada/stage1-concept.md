# Stage 1 — Concept (project inception, pre-tender)

The client has an idea for a rail tunnel-ventilation/station M&E SCADA system, or an oil & gas plant/field SCADA/ICSS, and needs a feasibility study. The **Consultant** is the primary actor at this stage; no Contractor is engaged yet.

## Sequence

1. Client hires a **Consultant** for feasibility.
2. Consultant runs the **initial survey and feasibility study** — for rail, this includes identifying which systems SCADA must supervise (tunnel-ventilation fans/dampers, station pumps, escalators/lifts status, HVAC) and whether the tunnel-ventilation fire/emergency-mode function is in scope; for O&G, an early review of the process scope, and whether a separate SIS/ESD system exists or is planned alongside this SCADA scope.
3. Consultant **collects requirements from stakeholders** — operations, maintenance, safety/HSE (critical if a fire/life-safety or SIS-adjacent function is in scope), other client departments, the regulator — and identifies which standards apply.
4. Consultant **floats queries to the market** (RFI-style, to SCADA/PLC/RTU OEMs and system integrators) to get **initial budgetary estimations**.
5. Consultant prepares an **initial high-level proposal**, including **options across different OEMs/platforms** (named generically here; never invent specific model data without a source).
6. This proposal, with the **price estimation**, goes into the **main project package** submitted for approval.

## Inputs

- Deployment context (rail tunnel-ventilation/station M&E vs O&G plant/field process control) and scope basics (number of tunnels/stations, or number of process areas/wellsites — order of magnitude)
- Whether a fire/life-safety emergency-mode function (rail) or a SIS/ESD interface (O&G) is in scope
- Hazardous-area classification, at least preliminarily, for O&G
- Greenfield vs brownfield (existing legacy SCADA/RTU estate present that needs replacing, integrating with, or migrating from?)
- Stakeholder requirements: operations, maintenance, HSE/safety, other client departments, regulatory bodies
- Applicable standards identified for this project/region
- List of OEMs/platforms to approach for market RFI, and what to ask them for (budgetary estimate basis)
- Who the proposal and price estimate go to for approval

## Decisions

Which OEMs/platforms to approach; which standards apply; high-level architecture direction (centralised SCADA vs distributed DCS-style architecture, if the client is open to discussing it at this stage); which options to present.

## Calculations

Order-of-magnitude/parametric only — approximate I/O point count from the number of field devices/systems to be supervised, approximate RTU/PLC count from site count. Not a detailed network or redundancy design yet.

## Deliverables

- Feasibility study report (including preliminary SIS-boundary or fire/life-safety-scope review where relevant)
- Stakeholder requirements register
- Initial high-level proposal, with OEM/platform options
- Budgetary price estimate
- Project approval package

## Roles

- **Consultant** — producer of all deliverables at this stage
- **Client** — requester and final approver of the package
- **OEM/Vendor** — responds to market queries with budgetary data
- **Contractor** — not engaged yet
