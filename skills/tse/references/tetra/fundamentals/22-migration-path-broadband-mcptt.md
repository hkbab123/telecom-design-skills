# Migration Path — Broadband PMR / MCPTT

TETRA's long-term succession direction, referenced by SKILL.md's Design Rule 5 — read this when a client's needs are pushing beyond what narrowband TETRA can deliver.

## Why a migration path exists at all

TETRA's throughput ceiling (fundamentals file 08 — SDS and modest packet data, no meaningful support for video, high-resolution imagery, or high-bandwidth telemetry) is a hard architectural limit, not a configuration choice. As client needs grow — body-worn cameras, real-time video from field incidents, high-volume sensor/telemetry data, integration with broader IT/data systems — narrowband TETRA structurally cannot deliver, and the industry-wide answer is migration toward broadband, LTE/5G-based mission-critical communication.

## Mission Critical Push-to-Talk (MCPTT)

A **3GPP-standardised** capability (not a TETRA/ETSI standard — a different standards body, reflecting the shift to cellular-technology-based mission-critical communication) that replicates PMR-style group-call/push-to-talk functionality over an LTE or 5G bearer, aiming to match or exceed TETRA's mission-critical call-setup speed and reliability while gaining broadband's throughput and IP-native data capability. MCPTT is the direct technical analogue of GSM-R's FRMCS succession path (also 3GPP/LTE-based) — the same industry shift (narrowband PMR standards giving way to 3GPP mission-critical standards) is happening in parallel across both the rail (GSM-R → FRMCS) and general PMR (TETRA → MCPTT/broadband PMR) domains.

## Deployment models for the migration

- **Dedicated private broadband network** — the client builds/operates its own private LTE/5G network for mission-critical use, the most control but the highest capital cost — realistic mainly for large asset owners (major rail networks, large O&G operators).
- **Hybrid/dual-mode terminals and networks** — TETRA remains for core mission-critical voice (proven reliability, no migration risk to core operations) while broadband is added alongside for data-heavy applications (video, high-volume telemetry) — often the pragmatic near/medium-term path, letting a client add broadband capability without a disruptive full TETRA replacement.
- **Commercial carrier-based mission-critical service** — using a public mobile carrier's network with mission-critical-grade service arrangements (priority access, dedicated mission-critical service tier), rather than building private infrastructure — lower capital cost, but dependent on carrier coverage and service commitments.

## Phased cutover from legacy communications to TETRA — a different migration, the opposite direction

Distinct from the TETRA→broadband succession path above: most TETRA projects are themselves a migration, from an existing legacy system (analogue VHF/UHF PMR, or an older trunked technology) onto the new TETRA network, and for a 24/7 operation (an active rail line, a continuously-running refinery) this cutover has to happen **without an operational gap**, not as a single flag-day switch-over. The standard technique is a **parallel-run cutover**:
1. **Build and commission the new TETRA network fully, in parallel with the legacy system still operating** — including coverage verification (testing/commissioning fundamentals file) before any user is moved onto it.
2. **Bridge the two systems** during the transition using the adjacent-network interface pattern described above (a patch/interconnect device, not deep protocol integration, since the legacy system likely isn't TETRA-standard) — so a user still on the legacy radio and a user already moved to TETRA can still reach each other during the changeover window.
3. **Migrate user groups in phases**, not all at once — typically by operational area or shift, each phase re-issuing terminals and retraining the affected group, verifying operational continuity before moving to the next phase, so a problem discovered in phase 1 doesn't disrupt the whole operation.
4. **Decommission the legacy system only after the last phase is confirmed stable** — keeping the bridge/patch interconnect live as a fallback until then, not removed the moment the last group nominally switches over.

The phasing plan (which groups/areas move in which order, and what the acceptance criteria are for moving to the next phase) is a project-specific operational decision the client's operations team needs to own jointly with the contractor — the network design can support a clean cutover, but the phasing sequence itself depends on the client's own operational risk tolerance and shift/outage windows.

## Why this matters for design decisions

- For any 24/7 or safety-critical operation, ask explicitly during Stage 1/2 whether a legacy system is being replaced and, if so, scope the parallel-run/bridging interconnect and phased-cutover plan as its own deliverable — don't leave a no-downtime requirement implicit and undesigned.
- Design Rule 5 says don't treat migration as out of scope by default — during Stage 1/2 intake, ask whether the client anticipates broadband/data needs (video, high-volume telemetry, IT integration) even if the immediate project is a straightforward voice network; if so, flag the hybrid/dual-mode path as worth scoping alongside the core TETRA design, not as a separate unrelated project.
- A pure TETRA design for a client that's about to need broadband capability risks becoming a stranded investment sooner than expected — worth surfacing this trade-off explicitly rather than silently designing only for today's stated requirement.
- This is a genuinely fast-moving area (3GPP MCPTT standards, commercial mission-critical carrier offerings, and private 5G practice are all still maturing) — treat any specific product/service claim here as needing current verification, more so than the stabilised TETRA/ETSI content elsewhere in this skill.

Formal reference: 3GPP TS 23.379 and related series (MCPTT); no ETSI TETRA standard covers this since it's explicitly the succession technology, not a TETRA feature.
