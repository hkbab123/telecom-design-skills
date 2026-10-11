# Power, Environment and Antenna Installation

## Why it matters

The antenna is the only part of the system outside and exposed. Lightning, wind and poor cable choice cause most real-world failures of otherwise sound designs.

## Power

- Masters and sub-masters on UPS or DC supply. Holdover protects against loss of the *reference*, not loss of *power*: a master that loses power loses its oscillator state, and a cold OCXO or rubidium unit takes time to stabilise after restart (`03`).
- Size autonomy for the longest credible mains outage, or ensure automatic restoration comes with time restored from a healthy peer before consumers re-sync.
- Display clocks: PoE from a UPS-backed switch or UPS-backed supply.

## Environment

- Equipment rooms: temperature and humidity within the master clock's rated range; a stable temperature helps oscillator holdover.
- Outdoor display clocks: ingress and impact ratings (`07`).
- Rail trackside rooms: EN 50125 environment classes and EN 50121 EMC (`10`).

## Antenna installation

1. **Mounting** — rigid mast or wall bracket; away from other antennas and metal structures that cause multipath; wind-load rated; accessible for maintenance with safe working at height.
2. **Lightning protection** — the antenna must sit within the protected zone of the building's lightning protection (IEC 62305), with a surge arrestor at the point where the cable enters the building, bonded to the earth reference. The arrestor adds delay to be recorded (`02`).
3. **Cable** — low-loss coaxial rated for the run length; if the run exceeds the receiver's allowed attenuation, add a line amplifier (also adds delay and needs power) or a fibre-optic antenna extender.
4. **Cable delay** — record the length and every inline element's delay; enter the total in the receiver (worked example in `02`).
5. **Grounding** — one bonded reference; avoid earth loops with the equipment-room ground.
6. **Redundancy** — two antennas on separate mounts for critical masters; a shared splitter reintroduces a single point of failure.
7. **Hazardous areas** — keep the antenna out of classified zones where possible (`11`).

## Common mistakes

- Antenna on a shared mast with high-power transmitters.
- No surge protection, or protection that is not bonded.
- Undocumented cable delay.
- One antenna splitter feeding both receivers.
- Treating UPS autonomy as equivalent to holdover.
