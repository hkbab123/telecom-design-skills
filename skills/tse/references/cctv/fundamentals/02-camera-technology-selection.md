# Camera Technology Selection

Camera type is chosen per coverage-zone *purpose*, not by default preference:

- **Fixed cameras** — the default for a defined, unchanging field of view (a platform edge, a doorway, a process area). Cheapest, simplest, most reliable.
- **PTZ (pan-tilt-zoom)** — for areas needing operator-directed follow-up (a large open yard, a perimeter with an operator actively tracking an incident). Needs a justified operational reason — PTZ coverage depends on someone pointing it at the right place at the right time, which fixed cameras don't.
- **Fisheye/panoramic** — wide-area coverage from a single mounting point (a concourse, a large room) where multiple fixed cameras would otherwise be needed; dewarped digitally at the VMS.
- **Thermal cameras** — for low/zero-light perimeter detection and, in O&G, early fire/hot-spot detection (see `fundamentals/11-og-perimeter-thermal-surveillance.md`). Not for general identification-quality coverage — thermal shows heat signatures, not recognisable detail.
- **Ex-rated (explosion-proof) cameras** — mandatory wherever a camera sits in a classified hazardous area (`fundamentals/08-hazardous-area-camera-certification.md`).

**Performance targets that actually matter:** resolution (megapixels) determines identification distance, not just "how sharp the image is" — a common mistake is specifying high resolution without checking it against the actual distance-to-target for that coverage zone's purpose (deterrence needs less resolution than facial/ANPR identification). Low-light/lux rating determines whether the camera is usable at night or in a tunnel without supplemental IR illumination — don't assume daylight performance figures apply after dark.

**Why this matters for design decisions:** camera-type mismatch (e.g. specifying PTZ where fixed would serve the stated purpose, or specifying thermal where identification-quality footage is actually needed) is one of the most common and expensive CCTV design errors — it shows up at Stage 2 item 5 and gets locked in by the time equipment is ordered at Stage 3.

**Formal reference:** IEC 62676-1 (camera/device classification), manufacturer datasheet lux/IR specifications (confirm with OEM — no unsourced figures).
