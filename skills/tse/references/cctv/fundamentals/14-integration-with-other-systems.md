# Integration with Other Systems

CCTV rarely stands alone — it's usually one input among several in a control room or security operation. The key interface families:

- **Detection/safety systems** (intrusion detection, fire/gas detection, PIDS) — the core integration pattern per `fundamentals/07-cctv-as-verification-not-detection.md`: a detection alarm auto-calls-up the relevant camera view for operator verification. The ICD needs to specify the exact trigger signal, protocol, and which camera(s) map to which detection zone.
- **PAGA** — a genuinely useful cross-subsystem pattern: a CCTV-verified security or safety event can auto-trigger a pre-recorded PAGA announcement (e.g. an evacuation message), or conversely a PAGA General Alarm activation can auto-call-up relevant camera views for the control room. Worth raising proactively on any project where both subsystems are in scope.
- **SCADA** — video verification of a SCADA process alarm (the operator sees the camera view alongside the SCADA alarm to visually confirm the condition before acting) — see the SCADA subsystem's `fundamentals/15-interfacing-other-systems.md` for the reciprocal view of this same interface.
- **Access control** — correlating access events (a badge swipe) with the corresponding camera view, typically the core PSIM correlation pattern where one exists.
- **Enterprise/incident-management systems** — exporting footage or metadata into an incident-management or evidence-management workflow, with the access-control/audit-trail discipline from `fundamentals/13-privacy-data-protection-retention.md` carrying through.

**What an ICD for a CCTV interface needs to specify:** the trigger condition and signal/protocol, which camera(s) respond and how (auto-call-up on an operator workstation, a specific video-wall tile, a recorded-clip export), any timing requirement (how quickly must the camera view appear after the trigger), and who owns testing that interface at FAT/SAT.

**Why this matters for design decisions:** these interfaces are usually where a CCTV design's real value is delivered on a live-operations project (an operator catching a real event because the right camera appeared automatically) — under-specifying them at Tender stage is a common way for a technically correct CCTV system to still underperform operationally.

**Formal reference:** no single unifying standard for cross-system integration — each interface is governed by the ICD agreed between the two system owners, informed by IEC 62676's VSS framing and the relevant standard for the other system (IEC 60839 for detection/alarm, IEC 60849/EN 54 for PAGA, IEC 62443/60870-5 for SCADA).
