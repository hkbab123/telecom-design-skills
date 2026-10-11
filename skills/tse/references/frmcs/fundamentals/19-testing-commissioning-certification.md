# Testing, Commissioning and Certification

## Why it matters

FRMCS is multi-vendor and standards-based, so interoperability cannot be assumed. Proof needs a layered test approach, from conformance in the lab to statistical performance on the line.

## Test layers

1. **Component and conformance tests** — equipment conformance to the pinned baseline; vendor test reports reviewed against the standard's conformance suites where they exist.
2. **Lab interoperability** — trackside radio, core, service platform, on-board gateway and key applications from the chosen suppliers tested together before field installation. Include negative cases (faults, congestion, authentication failures).
3. **Application tests** — end-to-end tests with the signalling system, control centre and other consumers (`18`).
4. **Field trials** — coverage and KPI measurement against the design, in each environment type: open line, cuttings, tunnels, stations, depots.
5. **Drive/ride tests at speed** — handover statistics at line speed, many runs, recorded conditions (`08`).
6. **Fleet testing** — on-board equipment tested per vehicle type; dual-mode fallback behaviour.
7. **Resilience tests** — failover of the core, site loss, backhaul cut, authentication-server loss (`15`).
8. **Security tests** — vulnerability scan, penetration test, SIM/credential lifecycle test (`16`).
9. **Migration tests** — interworking, bearer switching, cutover rehearsal and rollback (`13`).
10. **Regression after release changes** — a defined subset re-tested whenever software or baseline changes (`20`).

## Acceptance criteria

Write each as measurable: quantity, location, method, number of runs, statistic (for example a percentile), pass limit. "Handover shall be fast" is not testable; "the interruption time at 95th percentile shall not exceed X ms over N runs at line speed, measured at the on-board gateway" is.

## Certification and approvals

- Regulatory: spectrum licence conditions, type approvals, radio equipment compliance.
- Railway: on-board equipment approval for each vehicle type; signalling acceptance of the communication path; independent safety assessment where the allocation requires it.
- Interoperability: cross-border and cross-supplier interoperability evidence as required by the infrastructure manager or authority; verify current schemes.

## Evidence for later use

Keep raw measurement data, instrument and tool configurations, software versions and test environments. The signalling safety case and later disputes will ask for them.

## Common mistakes

- Field testing before lab interoperability.
- Single-run drive tests.
- Not freezing the software baseline for the acceptance campaign.
- No regression plan for future releases.
