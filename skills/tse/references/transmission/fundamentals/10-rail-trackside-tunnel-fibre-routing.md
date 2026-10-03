# Rail Trackside and Tunnel Fibre Routing

**Why this matters:** the rail environment decides physical diversity, repair time and cable life more than any technology choice.

## Typical route types

- **Trackside trough/duct (at-grade, cutting)** — exposed to vandalism, vegetation, drainage, track maintenance.
- **Viaduct/bridge** — cable tray or conduit on the structure; shared with other services; thermal movement at expansion joints.
- **Tunnel** — cable tray on tunnel wall; very constrained, one or two walls only; fire and smoke rules apply.
- **Station** — risers, equipment rooms, ODF locations; cable entry into the node room.

## Diversity in the rail context

- In a twin-bore tunnel, using one wall in each bore, connected at cross-passages, is a common way to obtain physically separate paths.
- Single-bore tunnels and viaducts often cannot offer true separation; the SRLG must be documented and a compensating measure agreed (fire-resistant cable, additional protection, short repair time).
- Cross-passage and bridge crossings are the classic shared points.

## Installation and protection

- LSZH cable in tunnels and stations (see `02`).
- Mechanical protection where the cable is within reach of maintenance activity.
- Segregation from traction power and high-voltage cable to limit induced interference (optical fibre is immune, but metallic armour and tracer wires are not); follow the project's segregation rules and EN 50121 EMC principles.
- Joint-closure locations accessible for repair without track possession where possible.

## Repair and maintenance

Repair time is dominated by access (possession windows) rather than splicing. Specify: spare cable length (slack loops), spare closures, location of repair stock, response contract. Record these in the availability model (see `stage2-tender.md` item 14).

## Fault location

OTDR (optical time-domain reflectometer) measurement locates the fault by distance; keep accurate route chainage and slack-loop records so distance converts to location.

## Common mistakes

- Treating two trays on one tunnel wall as two routes.
- Specifying repair time without possession constraints.
- Not recording slack loops and joint positions, making OTDR distance hard to translate into a physical location.
