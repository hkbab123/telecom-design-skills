# Security, Identity, SIM and Key Management

**Technical basis for Rule 7:** cybersecurity is first-class.

## Why it matters

An all-IP, standards-based platform with many tenants, remote management and interconnects exposes railway critical communications to threats that a closed circuit-switched radio network did not face in the same way. Security decisions made late are expensive; identity and key management in particular must be designed from the start.

## Security layers

- **Access security** — mutual authentication of the terminal and network (5G system security, TS 33.501), encryption and integrity protection of radio and core traffic.
- **Service security** — authentication and authorisation of the mission-critical service user, group security, end-to-end media/signalling protection and key management (TS 33.180).
- **Application-layer protection** — safety-related data protection by the signalling system (EN 50159, `12`); do not rely on the bearer alone.
- **Management plane** — secure administration, role-based access, logging.
- **Interconnects** — protection at the boundaries to other railway networks, public networks, roaming partners and control-centre systems.

## Identity and credentials

- **SIM / eSIM lifecycle** — who provisions, personalises, distributes, replaces and revokes credentials; logistics for fleets and portable devices; loss and theft handling. eSIM remote provisioning adds flexibility and a new attack surface.
- **Functional identity binding** — functional aliases (`03`) must be bound to authenticated users or devices with controlled login and logout.
- **Key hierarchy** — who holds root keys, where keys are stored (secure hardware), rotation, backup and recovery.

## Zone and conduit design (IEC 62443, CLC/TS 50701)

Separate zones for radio access, core, service platform, management, on-board, and interconnects; define allowed conduits with firewalls and monitored gateways. Apply railway cybersecurity risk assessment per CLC/TS 50701 to set target security levels.

## Operations

- Security monitoring and incident response integrated with the railway's operations centre.
- Patch and firmware management for a multi-vendor environment, including on-board equipment that is updated rarely.
- Penetration testing and vulnerability assessment before and after commissioning.

## Vendor and component compliance

Banned-vendor lists, sovereign-sourcing requirements and supply-chain assurance are spec-stage gates (Rule 9); check the actual selected equipment, not only the OEM name.

## Common mistakes

- Leaving SIM/eSIM lifecycle to the operations phase.
- Treating the mobile network's built-in security as sufficient for safety-related data.
- A flat management network reaching all sites.
- No revocation process for lost terminals.
