# OTN, DWDM and CWDM

**Why this matters:** wavelength multiplexing is the capacity and reach lever when fibre is scarce or spans are long; OTN adds a digital wrapper with strong OAM.

## WDM grids

- **CWDM (ITU-T G.694.2)** — 20 nm spacing, up to 18 channels in 1270–1610 nm; cheap, uncooled optics, limited reach, no amplification practical.
- **DWDM (ITU-T G.694.1)** — fixed grids of 100/50/25/12.5 GHz around 193.1 THz; 40–96 channels typical; supports amplification and long reach.

Use CWDM for a few extra services on constrained fibre (e.g. per-station dedicated wavelengths) and DWDM when aggregate capacity or reach demands it.

## OTN (ITU-T G.709)

A digital wrapper with its own framing, forward error correction and OAM. Containers: ODU0 (1.25 Gb/s), ODU1, ODU2, ODU3, ODU4, ODUflex. Benefits: client-agnostic mapping (Ethernet, SDH, others), strong monitoring (tandem connection monitoring), FEC to extend reach.

## Amplification and OSNR

- **EDFA** amplifiers extend spans; each adds noise.
- Long amplified systems are **OSNR-limited**: the design checks OSNR at the receiver against the required value for the line rate and modulation, with margin.
- **ROADMs** let wavelengths be added/dropped/switched remotely; relevant for multi-ring or branching networks.
- Coherent transceivers (100G and above) handle CD and PMD digitally, easing dispersion design.

## When this applies

Typical rail/O&G corridors rarely need long-haul DWDM; it appears on long pipelines, multi-site terminals and large national backbones. Check capacity forecast and fibre-availability before adding the cost and operational complexity.

## Common mistakes

- Selecting DWDM for capacity the fibre count could carry more cheaply.
- Ignoring that amplified sites need power, space and access along the route.
- Treating wavelength channels as automatically protected; protection is a design choice at the optical or OTN layer (see `07`).
