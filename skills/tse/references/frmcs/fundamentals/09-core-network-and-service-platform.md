# Core Network and Service Platform

## Why it matters

The core and the mission-critical service platform decide who can talk to whom, how traffic is prioritised, where data is processed and how the system survives failures. It is also where multi-vendor interoperability is hardest.

## Components (conceptual)

- **Core network** — 5G core (target) or EPC (LTE-based early deployments): authentication, session management, policy and QoS, mobility management, user-plane forwarding.
- **Mission-critical service servers** — the MCPTT/MCData/MCVideo application servers, group management, configuration management, key management (`03`).
- **IMS and signalling** — session control for voice/video services where used.
- **Identity and subscriber data** — subscriber database, functional identity mapping, authorisation (`16`).
- **Edge / user-plane placement** — where traffic breaks out. Placing the user plane near the access reduces latency and keeps critical traffic inside the railway domain, at the price of more distributed infrastructure.
- **Interconnect** — to other railway networks (cross-border), public networks (roaming/fallback), control-centre systems and gateways.

## Slicing and QoS

Network slicing offers logically separated networks over shared infrastructure with their own resources and policies. For a railway, a critical-communications slice and a separate performance/business slice are typical options (`10`). Whether slicing is mature enough on a given platform and release is something to confirm with the vendor and the pinned baseline.

## Design decisions

1. Core generation and release alignment with the standards baseline.
2. Service-platform scope: single vendor suite or best-of-breed with defined interfaces (and who integrates).
3. Placement of core and service sites, and user-plane/edge nodes.
4. Subscriber and identity architecture (including functional identities).
5. Interconnect design for cross-border, roaming and interworking (`13`).
6. Capacity and scalability: sessions, groups, simultaneous calls, signalling load.

## Redundancy preview

Geographic redundancy, active/active vs active/standby, and database replication are covered in `15`.

## Common mistakes

- Selecting a core without verifying support for the mission-critical service features the client relies on.
- Underestimating signalling load at shift changes and during incidents.
- Leaving interconnect and roaming as "later".
