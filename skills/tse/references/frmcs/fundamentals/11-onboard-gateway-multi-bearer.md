# On-Board Gateway and Multi-Bearer

**Technical basis for Rule 8:** on-board equipment is in scope.

## Why it matters

The train is half the system. The application KPIs are met or missed at the on-board interface, and retrofit across a mixed fleet is usually the longest-lead, highest-cost, most operationally constrained part of the programme.

## Role of the on-board gateway

An on-board communication gateway presents a common interface to on-board applications (train control, voice, video, diagnostics) and manages one or more bearers underneath: FRMCS on 5G NR or LTE, public-network access, legacy railway radio during transition, and optionally Wi-Fi at stations and depots or satellite. It handles:

- **Bearer selection and steering** by policy (application class, availability, cost).
- **QoS marking and traffic shaping** so critical flows keep priority.
- **Session continuity** across handovers and bearer changes.
- **Identity** — SIM/eSIM or equivalent credentials, functional-identity registration (`03`, `16`).
- **Local measurements and logging** of KPIs for acceptance and monitoring (`17`).

## Cab and application interface

- Driver's radio terminal/cab interface and its human-factors requirements.
- Interface to the train-control on-board unit (data path, QoS class, failure indications).
- Interfaces to on-board video, diagnostics and passenger systems.
- Interface to train management systems for status and alarms.

## Antenna design

- Number, placement and diversity (separation) of antennas for the cab link; roof-mounted antennas avoid carriage loss (`04`).
- Separate antennas for different bearers and bands; isolation between them.
- Environmental and mechanical requirements (EN 50155, EN 50125, EN 50121 EMC) and clearance gauge limits.

## Multi-bearer policy (hybrid delivery)

State which application classes may use which bearer. For example: critical flows only on the dedicated network; performance flows on the dedicated network with offload permitted; business flows on any bearer. The policy needs defined behaviour on loss of the dedicated bearer (fail to public network? alarm? stop?), which links to the safety communication boundary (`12`).

## Retrofit and fleet management

- Fleet inventory by type and age, space and power for the gateway, installation time per vehicle and downtime, type approval, and software update management.
- Mixed fleets during transition: some trains with the new gateway only, some with the legacy radio only, some dual (`13`).
- Spare gateways and SIM logistics.

## Common mistakes

- Specifying trackside KPIs without an on-board counterpart.
- Under-estimating retrofit lead time and homologation.
- No defined behaviour on loss of the dedicated bearer.
- Antenna isolation problems from co-located bearers on the roof.
