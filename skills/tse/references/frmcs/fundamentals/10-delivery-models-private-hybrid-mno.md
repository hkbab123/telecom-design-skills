# Delivery Models: Dedicated, Hybrid and MNO-Hosted

**Technical basis for Rule 2:** the delivery model is the first architectural fork.

## Why it matters

A legacy railway radio network is owned, built and operated by the railway or its contractor end to end. With FRMCS built on 3GPP technology that public operators also run, the railway can choose to own the network, share it, or buy it as a service. The choice drives control, risk, cost, timeline and what the contract must say.

## The options

| Model | What it means | Typical strengths | Typical risks |
|---|---|---|---|
| **Dedicated railway network** | Railway owns or controls the RAN, core and service platform | Full control of coverage, priority and security; independence from commercial changes | Highest capex and operating burden; must build all sites and skills |
| **Hybrid** | Dedicated critical network plus public-network bearers for non-critical or fallback traffic | Cost-efficient capacity for performance/business traffic; extra resilience for some flows | Two networks to manage; coverage and policy differences; gateway complexity (`11`) |
| **MNO-hosted / sliced service** | Operator delivers railway service on its network under SLA, possibly via a dedicated slice and priority | Lower capex, speed to deploy | Dependence on a commercial operator; coverage along the track and in tunnels may not match; SLA enforceability; contract life vs asset life |
| **Neutral host / shared infrastructure** | Sites or infrastructure shared between railway and operators | Reduces duplicate sites in tunnels and stations | Governance and interference management |

## What to compare

1. **Control** — who decides priority, pre-emption, changes and outages.
2. **Coverage along the track** — guaranteed by design or by SLA, including tunnels and cuttings.
3. **Availability and resilience** — what the SLA guarantees versus what the application KPIs need.
4. **Security and sovereignty** — who holds keys and subscriber data; regulatory constraints.
5. **Lifecycle** — contract term vs the railway's decades-long asset life; exit and re-tender terms.
6. **Cost model** — capex vs opex, including the operating organisation.
7. **Interoperability and cross-border** — roaming/interconnect with neighbours' models.
8. **Spectrum** — who holds the licence and under what conditions (Q1d).

## Typical engineering consequences

- Dedicated: full RF, capacity and core design in scope (this folder's sequences apply in full).
- Hybrid: add a multi-bearer on-board gateway design, bearer-selection policy and a policy for which traffic is allowed on the public bearer.
- MNO-hosted: the Tender spec becomes more of a service-level and acceptance specification; coverage and KPI verification obligations are central (`19`).

## Common mistakes

- Choosing the model on capex alone.
- Specifying a commercial SLA without a measurement and remedy method.
- Assuming the operator's public-coverage maps equal coverage along the track.
- Not planning the exit if the contract ends before the asset's life.
