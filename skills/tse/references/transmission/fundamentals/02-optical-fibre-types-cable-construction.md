# Optical Fibre Types and Cable Construction

**Why this matters:** fibre and cable are the longest-lived and hardest-to-change part of the system. Wrong fibre type or cable construction is a decades-long constraint.

## Single-mode fibre categories (ITU-T)

| Category | Typical use |
|---|---|
| G.652 (D) | Default standard single-mode fibre; backbone, rings, most O&G and rail |
| G.657 (A1/A2/B3) | Bend-insensitive; station/building entry, tight routing, fibre-to-equipment tails |
| G.655 | Non-zero dispersion-shifted; older DWDM long-haul; rarely chosen new |
| G.654 | Cut-off-shifted, low-loss; ultra-long-haul and subsea, rarely relevant here |

Default recommendation for new rail/O&G backbones: G.652.D for trunk cable, G.657 for patching and entry points. Verify against the client spec.

## Single-mode vs multimode

- **Single-mode (OS2)** — the backbone choice: long reach, high capacity, future-proof.
- **Multimode (OM3/OM4/OM5)** — short in-building or in-room runs only; never as backbone.

## Fibre count

Count = working fibres + protection fibres + spare (growth/repair) + reserve for other owners if the route is shared. Illustrative: spare of 30–50% of working is common, but project/client policy governs.

## Cable constructions

- **Loose-tube, gel-filled or dry** — most common for outdoor/duct/direct-buried; good for temperature variation.
- **Tight-buffered** — indoor/riser and short outdoor; easier termination.
- **Ribbon** — high fibre counts in a small cross-section; mass-fusion splicing.
- **Armoured (steel tape/wire)** — direct-buried, rodent protection, pipeline corridors.
- **Aerial (ADSS/OPGW)** — overhead; OPGW is combined with power ground wire on power lines.

## Fire, smoke and halogen performance

Tunnels, stations and enclosed plant need low-smoke zero-halogen (LSZH) sheaths. Relevant tests: flame propagation (IEC 60332 series), smoke density (IEC 61034), halogen/acid-gas emission (IEC 60754). Some jurisdictions add reaction-to-fire classes (e.g. the EU Construction Products Regulation, EN 50575) and rail-specific fire standards (EN 45545 for rolling stock). Fire-resistant (circuit-integrity) cable is a separate requirement for services that must survive a fire — confirm whether any transport route serves such a service.

## Common mistakes

- Choosing non-LSZH sheath for tunnel sections because it is cheaper per metre.
- Under-specifying spare fibre count, then paying a re-pull cost within a few years.
- Mixing fibre categories in one span without checking splice loss and mode-field mismatch.
