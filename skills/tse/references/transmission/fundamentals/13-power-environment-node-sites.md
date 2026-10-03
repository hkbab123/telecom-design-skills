# Power and Environment at Node Sites

**Why this matters:** transport nodes are only as available as their power and cooling; protection at the network layer is wasted if a node's power is a single point of failure.

## Power

- Telecom equipment commonly uses **-48 V DC** from rectifiers with battery backup; some modern equipment accepts AC or other DC voltages.
- Redundant rectifiers (N+1) feeding a battery bank and dual supply feeds to each node where the equipment supports it.
- **Autonomy** — battery time after mains loss, sized to the longest credible outage or until generator start. Illustrative: several hours at remote unmanned sites; confirm with client policy.
- Remote sites (pipeline repeaters, trackside huts) may need generators, solar or fuel cells; maintenance access then drives design.

### Worked example (illustrative)

A node draws 300 W at -48 V = 6.25 A. For 8 h autonomy: 6.25 A × 8 h = 50 Ah usable. With depth-of-discharge, ageing and temperature margins (e.g. 0.6 usable factor), nominal capacity ≈ 85 Ah. Real design uses the battery manufacturer's discharge curves.

## Environment

- Temperature and humidity control or ventilation per equipment rating; outdoor cabinets need thermal analysis.
- Dust, vibration, salt-mist (coastal/offshore) and condensation (tunnels) all matter.
- Space: ODFs, splice trays, cable slack, growth for future shelves.
- Fire protection and detection in node rooms; gaseous suppression is common for telecom rooms.
- Grounding and surge protection, bonded per the site earthing design; rail sites also consider traction-return and stray currents.

## Access and security

Node rooms are on the network's critical path; physical access control and logging belong to the design (see `14`).

## Common mistakes

- Single battery string or single feed for critical nodes.
- Sizing autonomy from the nominal, not the end-of-life, battery capacity.
- Ignoring maintenance access for remote unmanned sites.
