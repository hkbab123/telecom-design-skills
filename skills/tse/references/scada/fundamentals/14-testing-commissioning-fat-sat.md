# Testing & Commissioning — FAT/SAT Methodology

The method behind Stage 3 item 20 — read this when the question is "what does SCADA FAT/SAT actually involve," not just "decide the test plan."

## FAT vs SAT

**FAT** (Factory Acceptance Test) happens at the integrator's premises before shipment/deployment — the full SCADA system (servers, HMI, historian, and as many RTU/PLC panels as practical) is built up and tested as a system against a simulated or emulated field-I/O environment, catching integration defects before they're expensive to fix on site. **SAT** (Site Acceptance Test) happens after installation, retesting the same functional requirements against the real field devices and real network infrastructure, and adding tests that genuinely can't be done off-site (real cable runs, real RF/network conditions, real hazardous-area equipment as-installed).

## Loop testing

For every I/O point on the confirmed I/O list (Fundamentals file 02), a loop test verifies the signal path end-to-end: physically toggle/inject a value at the field device (or its simulated equivalent at FAT), confirm it reads correctly on the SCADA HMI with correct engineering units and correct tag identity — and, for outputs, confirm a command from the HMI correctly reaches and actuates the field device. This is tedious but non-negotiable — a single mis-wired or mis-mapped I/O point is a common and serious commissioning defect if not caught systematically.

## Emergency-mode / SIS-interface functional testing (the item most often shortcut, and the one that must not be)

Subsystem-specific rule 4 and the SIS-independence principle (Fundamentals file 07) both demand a dedicated test, separate from normal-mode loop testing: for rail tunnel ventilation, an actual fire-mode scenario simulation confirming the correct fan/damper sequence executes as designed for each defined fire-location scenario; for O&G, confirming the SIS-to-SCADA interface behaves exactly as specified (status/alarm surfaces correctly on SCADA, and any permitted override mechanism behaves within its designed constraints, nothing more). Treat this as its own signed-off test procedure in the FAT/SAT plan, not a checkbox folded into general functional testing.

## Cybersecurity configuration verification

Confirm the as-built network matches the IEC 62443 zone/conduit design (Fundamentals file 06) — firewall rule review, confirmation that no unauthorised direct IT-to-OT path exists, and (if in scope) a basic penetration/vulnerability scan appropriate to an OT environment (careful, non-disruptive scanning — a standard IT vulnerability scanner can crash fragile OT devices, so this needs OT-aware tooling/methodology, not a generic IT security test imported unchanged).

## Redundancy/failover testing

Actually trigger a failover (kill the active SCADA server, physically break a redundant network path) and observe the failover time and data continuity, rather than reviewing the redundancy design on paper and assuming it works (Fundamentals file 04).

## Why this matters for design decisions

- Stage 3 item 20's FAT/SAT plan should explicitly enumerate these distinct test categories (loop, emergency/SIS-interface, cybersecurity, redundancy) as separate signed-off procedures — a generic "system test" that doesn't separate them tends to under-test the categories that matter most in an actual incident.
- FAT catches defects when they're cheapest to fix; SAT catches defects FAT genuinely cannot (real cable plant, real hazardous-area installation) — neither substitutes for the other.

Formal reference: no single governing standard for SCADA FAT/SAT specifically; general systems-integration testing practice, informed by IEC 61508/61511 (for safety-interface testing rigour) and the project's own fire/life-safety code (for emergency-mode test acceptance criteria).
