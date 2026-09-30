# Video Surveillance System Architecture

IEC 62676 frames a video surveillance system (VSS) as four layers: **cameras** (image capture), **transmission network** (IP network carrying video streams), **video management** (VMS — recording, viewing, analytics, user management), and **storage** (NVR/SAN, short-term and archival). Each layer has its own design decisions, but they're not independent — a decision at one layer (e.g. codec choice) reshapes requirements at the others (network bandwidth, storage capacity).

**Centralised vs distributed VMS.** A centralised VMS puts all recording/management at one site — simpler to administer, but every camera's video must traverse the network to reach it, and a single-site failure is a bigger loss. A distributed VMS records locally (edge NVRs at each site) and federates viewing/management centrally — more resilient, more complex to administer, and the natural fit for geographically spread rail lines or multi-site O&G assets where backhaul bandwidth is limited or expensive.

**PSIM (Physical Security Information Management)** sits above the VMS layer where CCTV is one of several security subsystems (access control, intrusion detection, perimeter detection) that need a unified operator view and cross-system correlation (e.g. an access-control alarm auto-calls up the nearest camera). Not every project needs a PSIM — it's justified when there are enough separate security subsystems that an operator can't reasonably monitor them as separate screens.

**Why this matters for design decisions:** the architecture choice made here (centralised/distributed, PSIM or not) is the frame every later Tender-stage decision sits inside — network design, redundancy targets, and interface requirements all depend on which architecture was chosen, so this has to be settled early, ideally at Concept.

**Formal reference:** IEC 62676-1 (general requirements), IEC 62676-4 (application guidelines).
