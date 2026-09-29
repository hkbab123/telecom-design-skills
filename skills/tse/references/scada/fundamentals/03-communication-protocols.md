# SCADA Communication Protocols

The method behind Stage 2 item 8 — read this when the question is "which protocol should I actually specify," not just "decide the protocol."

## The two communication legs

SCADA communication happens on two distinct legs, usually with different protocols: **field-to-RTU/PLC** (sensors/actuators to the controller — often hardwired I/O or a fieldbus, not usually a "SCADA protocol" in the sense discussed here) and **RTU/PLC-to-SCADA** (the controller reporting up to the supervisory system — this is where the protocol choice in Stage 2 item 8 matters most).

## Modbus (RTU/TCP)

The simplest and most widely supported protocol — a master/slave (client/server) polling model, register-based data model, no built-in security. Good for straightforward point-to-point or small polled networks; its lack of native security and lack of a standard "report by exception" model (everything is polled, nothing pushed) are its main limitations at scale.

## IEC 60870-5-101 / -104

The telecontrol protocol family most common in rail/utility SCADA and increasingly O&G telemetry, especially outside North America. -101 is the serial variant, -104 is the TCP/IP variant. Supports "report by exception" (RTU reports a change when it happens, rather than only responding to a poll) and time-stamped events — a materially better fit than Modbus for event-driven alarm/status reporting over a wide-area network, which is why it's a common default for rail tunnel-ventilation and station SCADA telecontrol links.

## DNP3

A broadly similar telecontrol protocol to IEC 60870-5, more common in North American utility/O&G SCADA. Also supports report-by-exception and time-stamping; has a security extension (Secure Authentication) that is worth specifying explicitly if selected, since the base protocol (like Modbus and un-extended IEC 60870-5) has no native security.

## OPC-UA

A newer, platform-independent, service-oriented protocol with built-in security (authentication, encryption) and a richer information model than the register/point-based protocols above. Increasingly the choice for SCADA-to-historian, SCADA-to-MES, and multi-vendor Level 2/3 integration where a modern, secure, self-describing data model is wanted — less commonly the field-RTU-to-SCADA leg's protocol on brownfield/legacy sites, but increasingly specified on greenfield ones.

## The security gap common to the legacy protocols

Modbus, base IEC 60870-5, and base DNP3 were all designed in an era before OT cybersecurity was a serious design concern — none has native authentication or encryption. This is exactly why Stage 2 item 6 (IT/OT segmentation, IEC 62443) exists as a separate, mandatory item: protocol-level insecurity is compensated for by network-level segmentation and access control, not ignored.

## Why this matters for design decisions

- The protocol choice in Stage 2 item 8 should follow from (a) what the field-device population and any existing brownfield protocol already use, and (b) whether report-by-exception/event time-stamping is actually needed (usually yes, for alarm-driven rail/O&G SCADA) — not from habit or a single vendor's default.
- Never assume a protocol carries its own security — that's the segmentation fundamentals file's job, not the protocol's.

Formal reference: IEC 60870-5 series, IEEE 1815 (DNP3), IEC 62541 (OPC-UA), Modbus Organization specification.
