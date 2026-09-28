# Security, Encryption & Key Management

The technical mechanics behind Stage 2 item 11 — read this when the question is "how does TETRA encryption actually work," not just "which algorithm to pick."

## Two layers of encryption

TETRA security operates at two independent layers, and a project can use either or both:

- **Air-interface encryption** — encrypts the radio link between terminal and base station only; once traffic reaches the SwMI, it travels in the clear through the network core (unless end-to-end encryption is also applied). Protects against radio eavesdropping but not against interception inside the network infrastructure.
- **End-to-end (E2E) encryption** — encrypts traffic from the originating terminal all the way to the receiving terminal(s), including transit through the SwMI, so even network operator personnel cannot intercept clear traffic. Typically layered on top of air-interface encryption, not a replacement for it. Adds terminal processing overhead and requires an E2E key management infrastructure separate from the network's own authentication — usually reserved for security/emergency-response talkgroups where the extra complexity is justified, not applied network-wide by default.

## TEA algorithms (air-interface layer)

**TEA1–TEA4** are the standardised air-interface encryption algorithms, differing in strength and export/regulatory status:
- Different jurisdictions restrict which TEA variant may be used or exported — this is why Stage 2 item 11 says "confirm rather than assume": the applicable algorithm is a regulatory question as much as a technical one, decided by national security/export-control policy, not by network design preference.
- The algorithm choice doesn't change the network architecture — it's a configuration parameter on terminals and the SwMI's encryption engine, not a structural design decision.

## Authentication

Separate from encryption: **authentication** verifies a terminal is legitimate before it's allowed onto the network at all (preventing a stolen or cloned terminal from registering), using a shared secret key programmed into both the terminal and the SwMI's authentication centre. This happens at every registration, independent of whether encryption is subsequently used on the call itself.

## Over-the-air rekeying (OTAR)

Encryption keys need periodic replacement (for security hygiene, or to revoke a compromised/lost terminal's access). **OTAR** lets the SwMI push new keys to terminals over the air rather than requiring physical reprogramming of every radio — essential for any fleet beyond a handful of terminals, since manual rekeying doesn't scale. Key management policy to confirm with the client: rekeying frequency, and the process for immediately revoking a lost/stolen terminal's keys (a lost terminal with a valid key is a live security exposure until revoked).

## Why this matters for design decisions

- E2E encryption is a talkgroup-by-talkgroup decision, not a network-wide default — ask which specific groups (security, emergency response) actually need it, since it adds cost and terminal complexity.
- TEA algorithm selection needs a regulatory answer, not a technical preference — flag this to the client's compliance/security function rather than choosing unilaterally.
- OTAR capability should be confirmed as an actual requirement in the technical specification (Stage 2 item 11) — without it, a fleet of any real size becomes operationally difficult to rekey or to revoke a lost radio from.

Formal reference: ETSI EN 300 392-7 (security architecture, including TEA algorithms, authentication, OTAR).
