# Handover Mechanics — GSM-R's Most Safety-Critical Design Constraint

Why EIRENE's <300ms handover requirement exists and what actually drives meeting it — read this when the question is "why does handover matter so much for GSM-R," not just "design for fast handover."

## Why handover is different for GSM-R than for any general PMR/cellular network

A train moving at line speed (potentially 200+ km/h on high-speed lines) crosses cell boundaries far more frequently, and far faster, than a pedestrian or vehicle user on a general PMR or public cellular network. If a handover fails or takes too long, the driver or signalling-relevant voice/data link drops — and because GSM-R can carry safety-relevant communication (including, in some deployments, being the bearer for ETCS signalling data), a dropped call during a critical moment has direct operational-safety consequences. This is the entire reason EIRENE specifies a strict **handover completion target of under 300 milliseconds**, far tighter than any general cellular or PMR handover requirement.

## Standard GSM handover procedure

As in any GSM network: the terminal (or network, depending on measurement mode) monitors serving-cell and neighbour-cell signal quality; when a neighbour becomes sufficiently stronger, the network initiates a handover — instructing the terminal to retune to the new cell's channel, with a brief signalling exchange completing the handoff. GSM-R uses this same standard procedure — the railway-specific work is in **how the network is engineered and parameterised** to make this procedure complete reliably within 300ms at train speed, not a different handover protocol.

## What actually achieves the <300ms target

- **Cell overlap** — adjacent cells are planned with substantial overlap (well beyond what a general cellular network would use) so a train has ample time, even at line speed, to complete the handover procedure while still within the overlap zone — insufficient overlap is the single most common root cause of handover failure at speed.
- **Handover parameter tuning** — thresholds and hysteresis margins (how much stronger a neighbour must be, and for how long, before triggering handover) are tuned tighter/faster than typical public-GSM defaults, trading off against a higher tolerance for occasional unnecessary handovers in exchange for reliably fast ones.
- **Network-side processing speed** — the BSC's handover decision and execution speed itself needs to be fast enough to fit within the 300ms budget alongside the radio-layer signalling time — an OEM/equipment performance characteristic to verify, not assume.
- **Cell size vs train speed relationship** — the maximum sustainable train speed for a given cell size (and vice versa) is a direct engineering relationship: smaller cells reduce dwell time in the overlap zone, requiring a faster handover; larger cells (with correspondingly larger overlap zones) give more time margin but need more transmit power/height to maintain link quality across the larger cell. High-speed lines generally need this relationship explicitly calculated and verified against the actual design speed, not assumed to "just work" from a generic cell-planning approach.

## Why this matters for design decisions

- Cell/site spacing along the corridor (part of the coverage philosophy decision in Stage 2) should be explicitly checked against handover-time feasibility for the line's actual maximum train speed, not decided purely from a coverage-only link budget — a design that closes the link budget everywhere can still fail on handover timing if cell overlap is insufficient.
- Handover parameter tuning is a real, verifiable network-configuration deliverable — Stage 3's detailed design should include explicit handover-parameter settings and the evidence/calculation behind them, not just a statement that "fast handover is implemented."
- This is the GSM-R design constraint with the most direct safety consequence of any single technical decision in this skill — worth treating with more rigour than almost any other single item in the Stage 2/3 sequences, and worth flagging explicitly to Harish as a candidate for a dedicated checklist item if the current draft sequences don't already call it out with this level of emphasis.

Formal reference: EIRENE FRS/SRS (the <300ms handover requirement itself); 3GPP GSM handover procedures (the underlying mechanism EIRENE's requirement is layered onto).
