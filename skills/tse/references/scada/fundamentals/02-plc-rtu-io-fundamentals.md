# PLC/RTU and I/O Fundamentals

The method behind Stage 2 item 9 and Stage 3 item 4 — read this when the question is "how do I actually size the I/O list," not just "decide the I/O count."

## PLC vs RTU

A **PLC** (Programmable Logic Controller) executes cyclic control logic (IEC 61131-3 languages — ladder, structured text, function block) at a fast, fixed scan rate, typically close to the process, and is the more common choice where continuous local control logic is needed (a plant process area, a tunnel-ventilation fan group). An **RTU** (Remote Terminal Unit) is historically more oriented toward data acquisition and simple control over a communication link to a distant SCADA master, often at more relaxed polling intervals — common at dispersed sites (pipeline valve stations, wellsites) where the "local intelligence" requirement is lower than a process plant. Modern hardware increasingly blurs the line (many devices marketed as RTUs run full IEC 61131-3 logic), but the design question — how much autonomous local logic does this site need versus how much can rely on the SCADA link — still matters.

## Scan cycle

A PLC's scan cycle repeats continuously: read inputs → execute logic program → write outputs → housekeeping (communications, diagnostics) → repeat. Scan time (typically single-digit to tens of milliseconds for a modern PLC) sets the fastest rate at which the PLC can respond to a field-input change — a safety-relevant fast process (not the SIS, which has its own independent scan) or fast motor-control application needs a scan time well below its response-time requirement; a slow-changing signal (tank level, temperature) does not.

## I/O types

- **Digital Input (DI)** — on/off status (limit switch, motor running feedback, alarm contact).
- **Digital Output (DO)** — on/off command (start/stop a motor, open/close a valve/damper).
- **Analogue Input (AI)** — continuous measurement, most commonly 4-20mA current loop (chosen specifically because a broken-wire condition reads as 0mA, distinguishable from a valid "0%" reading at 4mA — a live-zero design principle worth knowing when someone asks "why 4-20mA and not 0-20mA").
- **Analogue Output (AO)** — continuous command (valve position, variable-speed drive setpoint).

## Building the I/O list (the method behind Stage 3 item 4)

1. List every field device from the Stage 2 scope (item 1) that needs monitoring or control.
2. For each, classify the signal type(s) it needs (DI/DO/AI/AO) — a single physical device (e.g. a motorised damper) often needs several: DI for open/closed limit switches, DO for open/close command, DI for a fault/trip status.
3. Sum by type per RTU/PLC panel to get a raw I/O count.
4. Add a spare-capacity margin (commonly 10-20%, but this is a client/project decision, not a fixed rule — state it explicitly rather than assuming a figure) for future expansion.
5. This raw count, plus the spare margin, sizes the I/O card/module count for each panel in Stage 3 item 11's equipment dimensioning.

## Why this matters for design decisions

- Getting the I/O list wrong (missing a signal, wrong type) is the single most common source of late-stage rework in a SCADA project — build it carefully at Stage 3 item 4, working from a confirmed field-device list, not a guess.
- The scan-cycle/response-time relationship is why "how fast does SCADA respond" is really two separate questions: PLC scan time (local, fast) and SCADA polling interval (over the network, slower — see the communication-protocols fundamentals file).

Formal reference: IEC 61131-3 (PLC programming languages).
