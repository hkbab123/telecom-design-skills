# Rail Station, Platform, and Tunnel CCTV

Rail CCTV has three distinct environments, each with its own design constraints:

**Station/concourse CCTV** — the most "standard" environment: good ambient lighting, stable mounting structures, relatively benign EMC environment. Purpose is typically a mix of deterrence, passenger-flow monitoring, and evidentiary record.

**Platform CCTV** — adds platform-edge monitoring (a passenger-safety purpose — detecting someone on the track side of the platform edge, supporting but not replacing any dedicated platform-intrusion detection system, per `fundamentals/07-cctv-as-verification-not-detection.md`) and typically needs coverage of the full platform length with overlap at the ends.

**Tunnel CCTV** — the hardest environment: low/zero ambient light (needs IR illumination or thermal supplementation), significant vibration from passing trains (affects mounting-bracket and camera-body robustness), and EMC interference from traction power systems (25kV AC or third-rail DC, depending on the line) which can affect both camera electronics and network cabling if not properly shielded/earthed. Tunnel cameras also typically need a harder ingress-protection (IP) rating against dust and moisture than station cameras.

**The evidentiary/passenger-safety role** is the dominant design driver across all three — unlike O&G's more security/process-monitoring-led CCTV purpose, rail CCTV specification is very often shaped by a transit authority's passenger-safety and law-enforcement evidentiary requirements (identification-quality resolution at key points, synchronized timestamping, defined retention periods tied to incident-investigation timelines).

**Why this matters for design decisions:** the tunnel environment in particular changes camera-technology selection (fundamentals/02) and network design (EMC-hardened cabling, fundamentals/05) in ways a station-only design wouldn't anticipate — always ask explicitly whether tunnel coverage is in scope before finalising equipment selection.

**Formal reference:** IEC 62676 (general VSS), national rail EMC/safety standards (e.g. EN 50121 series for railway EMC — confirm the applicable national standard per project), transit-authority-specific passenger-safety/CCTV design guidelines where they exist.
