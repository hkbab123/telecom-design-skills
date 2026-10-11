# Redundancy, Resilience and Availability

## Why it matters

A critical communication network is judged by how it behaves when something fails. Availability targets are set per application; redundancy is allocated to meet them and checked for hidden shared dependencies.

## Layers of resilience

- **Core and service platform** — geographic redundancy (two or more sites), active/active or active/standby, database replication, defined recovery time and data-loss tolerance. Check that signalling and user-plane paths are both protected.
- **Radio access** — overlapping coverage so loss of a site leaves service available (often by overlapping sites on a linear route, or by designing each point to be covered by two cells); power and backhaul diversity at each site.
- **Backhaul** — physical diversity and fast protection (`14`).
- **On-board** — dual radios or dual antennas and bearer redundancy (`11`).
- **Power** — battery and generator autonomy for sites, with a defined autonomy in hours based on repair time.
- **Management and security systems** — authentication servers, SIM management and key servers must be as resilient as the core they protect (`16`).

## Availability arithmetic

Availability of independent elements in series multiplies: A = A1 × A2 × …. For a parallel (redundant) pair, unavailability multiplies: U = U1 × U2, if failures are independent.

**Worked example:** a site with availability 0.999 (about 8.8 h downtime/year) with a redundant overlapping neighbour of the same availability gives U = 0.001 × 0.001 = 10⁻⁶, i.e. availability 0.999999, provided failures are independent. The independence assumption is the weak point: a shared backhaul duct, shared power feed, shared software defect or shared management system makes the true value much worse (common-cause failures).

## Common-cause checklist

Shared duct or trench, shared power, shared software version (a defect can hit both units at the same time), shared clock reference, shared management network, shared operators' procedures.

## Failure-mode review

For each failure (site, core node, link, management server, authentication server, on-board gateway), state the expected behaviour: what is lost, what continues, how long recovery takes and what alarms appear.

## Design decisions

1. Availability target per application.
2. Redundancy allocation by layer, with a common-cause review.
3. Overlapping coverage policy.
4. Recovery time objectives for the core and the management systems.
5. Repair and spares strategy (MTTR assumptions).

## Common mistakes

- Redundant core nodes in the same building or on the same power feed.
- Treating a redundant pair as independent without a common-cause review.
- Protecting the radio path but not the authentication or key-management servers.
- Quoting a network availability figure without stating the application it applies to.
