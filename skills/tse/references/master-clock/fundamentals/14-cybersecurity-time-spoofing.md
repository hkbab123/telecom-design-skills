# Cybersecurity and Time Spoofing

## Why it matters

Time underpins authentication (certificates, tokens), log integrity, and incident evidence. An attacker who can shift your time can expire certificates, defeat log correlation, or hide an event. Time systems are also quietly exposed: NTP servers answer anyone who can reach them.

## Attack surface

| Surface | Threat | Mitigation |
|---|---|---|
| NTP service | Spoofed or malicious server; reflection/amplification abuse of an open server | Restrict who may query; authentication (symmetric keys, NTS); no unauthenticated public exposure |
| PTP | Rogue grandmaster takes over through BMCA; message injection | Port roles fixed (master-only/slave-only), priority settings, filter PTP at the boundary, authentication where the profile supports it |
| GNSS | Jamming and spoofing | Layered mitigations in `02`: monitoring, cross-check, rate limits, holdover |
| Management plane | Weak credentials, default services, outdated firmware | Disable unused services (Telnet, HTTP), role-based access, firmware baseline |
| Supply chain | Components from a restricted vendor | Vendor compliance check (Rule 8) |

## Zone and conduit design (IEC 62443)

- Place the master clock in a defined security zone; define the conduits through which consumers reach it (NTP/PTP/IRIG), and which management access is allowed.
- Keep IT time and OT time separated where the client's policy requires it; if bridging, use a one-way or controlled path so OT is not exposed to IT-side faults.
- Never allow OT consumers to use external internet time sources.

## Design decisions

1. Which consumers can authenticate (NTS or keys) and which cannot; compensate for those that cannot with network controls (VLAN, ACL).
2. PTP port roles, grandmaster priority and clock-class settings so that no unauthorised device can win the BMCA.
3. How GNSS-spoof detection is reported and who acts on it.
4. Firmware update policy and the signed-image requirement.
5. Logging of administrative access.

## Vendor and constellation compliance

Same as the other subsystems: confirm banned-vendor-list restrictions before the OEM shortlist, and check any requirement about which GNSS constellations a receiver may use.

## Common mistakes

- NTP server open to anyone on the corporate network.
- Default credentials on web interfaces.
- No logging of time-setting changes.
- Allowing a device to be both a PTP master and a consumer by default.
- Assuming GNSS is trusted because it is "from space".
