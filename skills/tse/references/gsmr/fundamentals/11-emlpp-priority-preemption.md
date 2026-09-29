# eMLPP Priority & Pre-emption Mechanics

How GSM-R's priority system actually protects safety-relevant calls — read this when the question is "how does priority/pre-emption work," not just "decide the priority scheme."

## What eMLPP is

**eMLPP (enhanced Multi-Level Precedence and Pre-emption)** is a standard 3GPP GSM feature GSM-R relies on heavily: every call is assigned a priority level, and when network resources (traffic channels) are scarce, a higher-priority call attempt can **pre-empt** — forcibly terminate — a lower-priority call in progress to free a channel. This is the actual mechanism that makes a statement like "emergency calls always get through" technically true, rather than just an operational aspiration: pre-emption is what guarantees it even under full network congestion.

## EIRENE's defined priority levels

EIRENE specifies a defined set of priority levels mapped to railway operational call types — from lowest (general/non-operational traffic) to highest (railway emergency calls) — with intermediate levels for different classes of operational traffic (e.g. general operational calls, calls involving a specific train's safety-relevant communication, signaller calls). The exact level definitions and their mapping to call types are an EIRENE FRS/SRS-defined scheme, not a locally invented priority list — confirm the current EIRENE specification's exact level definitions for a given project rather than assuming a fixed scheme, since it's the kind of detail that benefits from checking against the current specification revision.

## How pre-emption actually executes

When a higher-priority call attempt finds no free traffic channel, the network identifies a lower-priority call currently in progress on that cell, terminates it (the pre-empted call's user experiences an abrupt call drop, typically with some indication that pre-emption occurred, though exact terminal behaviour is OEM-specific), and immediately assigns the freed channel to the higher-priority call attempt. This is a real, capacity-affecting network behaviour — not just a queueing/priority-scheduling scheme — and directly interacts with the Erlang-B capacity planning covered in the trunking fundamentals file: the blocking-probability target from that calculation effectively applies to the lower-priority traffic classes, since the highest-priority class is protected by pre-emption rather than by raw capacity margin alone.

## Why this matters for design decisions

- Priority-level assignment (which call type maps to which eMLPP level) is a genuine design decision with real operational and safety consequences — it should be confirmed against the current EIRENE specification and the client's own operational rules, not assumed from a generic template.
- Capacity planning (trunking fundamentals file) should explicitly account for pre-emption's effect on the traffic model — don't treat blocking probability as uniform across all priority classes when eMLPP pre-emption is in use.
- If a client or reviewer asks "what guarantees an emergency call always connects," the accurate technical answer is the eMLPP pre-emption mechanism specifically, not just "the network has capacity" — capacity headroom reduces how often pre-emption needs to trigger, but pre-emption is the actual guarantee mechanism.

Formal reference: 3GPP GSM eMLPP specifications (the underlying mechanism); EIRENE FRS/SRS (the specific priority-level scheme and call-type mapping GSM-R uses).
