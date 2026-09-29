# Fire & Gas / ESD Integration Mechanics

Underpins Stage 2 item 13 (life-safety interface family) and Stage 3 item 12 (the F&G/ESD Interface Control Document) — read this for how GA activation actually gets triggered automatically by another system, rather than only by a human operator.

## Why this interface is the most safety-critical one PAGA has

On an O&G facility, the whole point of the General Alarm function is often to respond automatically and immediately to a confirmed fire or gas-release event — waiting for a human operator to notice a fire panel alarm and manually trigger GA adds delay a genuine emergency can't afford. This makes the **Fire & Gas (F&G) detection system** and **Emergency Shutdown (ESD) system** interface the single most operationally important connection PAGA has, and the one that deserves the most rigorous Interface Control Document (ICD) of any interface family in Stage 2 item 13.

## Two integration mechanisms: hardwired vs digital bus

- **Hardwired (volt-free contact) interface** — the F&G/ESD system closes (or opens) a dedicated relay contact on confirmed detection, wired directly to a PAGA input that triggers a specific pre-programmed GA response (e.g. contact closure → play the standard evacuation message in the affected zone group). Simple, robust, and easy to verify functionally (you can literally see the relay close), but limited to whatever discrete signals were wired — no rich data about which detector triggered or where exactly.
- **Digital/serial bus interface** (e.g. Modbus, or an OEM-proprietary protocol) — the F&G/ESD system communicates richer event data digitally (which zone, which detector type, event severity), letting PAGA select a more specific, zone-targeted response than a hardwired contact alone could trigger. More capable, but depends on both systems' communication link staying healthy — meaning the interface itself needs its own supervision/health-monitoring, a genuinely different failure mode than a hardwired contact has.

Which mechanism a specific project uses is OEM- and vendor-integration-specific — confirm with both systems' vendors during Stage 3 item 2 (vendor document intake), and don't assume one mechanism's simplicity or richness without checking the actual interface capability of both systems being connected.

## The cause-and-effect matrix — the document that actually defines behaviour

The behaviour of this interface — which specific F&G/ESD trigger causes which specific PAGA zone(s) to receive which specific message — is documented in a **cause-and-effect matrix**: a table mapping each detection scenario to its required PAGA response. This matrix is typically owned by the fire engineering/process-safety function (not PAGA design alone) since it encodes the facility's overall emergency-response philosophy (does a gas release in Zone A trigger evacuation only in Zone A, or the whole facility? does a confirmed fire escalate the response after a set delay if not acknowledged?) — PAGA's Stage 3 item 12 ICD needs to faithfully implement whatever this matrix specifies, not invent its own response logic.

## Activation timing

The interface should have a defined, tested **activation timing** — how quickly after F&G/ESD confirms an event does the corresponding GA message actually begin playing. This is a genuine performance requirement worth specifying numerically (an illustrative example: within a few seconds of contact closure/digital trigger receipt) and verifying during commissioning (Stage 3 item 18's F&G/ESD-triggered activation test) — a technically correct interface that's simply too slow doesn't meet the actual safety intent.

## Why this matters for design decisions

- Stage 2 item 13 should identify hardwired vs digital-bus interface mechanism as an explicit open question to resolve with both systems' vendors, not assumed.
- Stage 3 item 12's ICD must be built directly from the facility's cause-and-effect matrix (typically a fire-engineering deliverable, not a PAGA-original document) — confirm this matrix exists and is current before finalising the ICD.
- Activation timing should be a stated, numeric requirement and a dedicated commissioning test item — this is the interface most likely to be assumed working without ever being actually tested end-to-end before an incident forces the question.

Formal reference: no single standard governs this specific interface's mechanics; IEC 61511 (where the overall F&G/ESD/GA chain is part of a SIL-rated safety instrumented function, fundamentals file 07) and the client's own fire engineering cause-and-effect documentation are the actual governing basis, confirmed per project.
