# Security & Encryption

The technical mechanics behind GSM-R's security layer — read this when the question is "how does GSM-R protect calls," not just "confirm encryption is enabled."

## Air-interface encryption

GSM-R uses standard **GSM A5 encryption algorithms** (the same family used in public GSM, e.g. A5/1, with algorithm choice/strength subject to the same kind of jurisdiction-dependent regulatory considerations as any cellular encryption scheme — confirm applicable requirements per project, never assume). This protects the radio link between terminal and BTS from eavesdropping; as with any GSM-family system, traffic within the core network beyond the air interface is not inherently encrypted by this mechanism.

## Authentication

Standard GSM SIM-based authentication (challenge-response using a shared secret key on the SIM and in the HLR/authentication centre) verifies a terminal is legitimate before network registration — the same mechanism as public GSM, extended in GSM-R by the functional-number login process (a user logging into a functional number is a separate operational-layer authentication step on top of the underlying SIM/network authentication, verifying the person is authorised for that operational role).

## Why GSM-R's security model is generally considered adequate but dated

GSM-R inherits 2G GSM's security architecture, including its known cryptographic limitations relative to more modern (3G/4G/5G) authentication and encryption schemes. This is a genuine, publicly acknowledged industry consideration in GSM-R's long-term position, and is one of the drivers (alongside capacity and data-bearer bandwidth limitations) behind the industry move to **FRMCS** (see the migration-path fundamentals file), which is designed on a modern, LTE/5G-based security architecture from the outset.

## Why this matters for design decisions

- Encryption/authentication configuration should be confirmed against the specific national railway administration's security policy and regulatory requirements — this is a policy/regulatory confirmation, not a technical default to assume uniformly across projects or countries.
- When a client or reviewer raises GSM-R's security model as a concern, the accurate answer is that it reflects 2G-generation cryptography (a known, industry-acknowledged characteristic) and that FRMCS is the planned modernisation path — not a claim that GSM-R's security is equivalent to modern cellular standards.
- Functional-number login (fundamentals file 07) should be treated as a distinct operational-authentication layer from network-level SIM authentication — both matter, and conflating them risks under-specifying one or the other in a technical requirement.

Formal reference: 3GPP GSM security specifications (A5 algorithm family, SIM authentication) — standard GSM, not railway-specific; EIRENE FRS/SRS for the functional-number login/authorisation layer.
