# Bandwidth and Storage Calculations

The core CCTV sizing formula — never assume an NVR/storage figure, show this calculation (rule 4):

**Per-camera bitrate** depends on resolution, frame rate, codec, and scene complexity (a busy platform needs a higher bitrate than a static corridor at the same resolution/fps, because compression works harder on motion). Manufacturers publish typical bitrate tables per resolution/fps/codec combination — use the OEM's published figure, don't invent one.

**Worked example:**
- Camera: 4MP (2688×1520), 25 fps, H.265, typical/moderate-complexity scene → OEM datasheet figure: ≈ 6 Mbps sustained bitrate.
- Storage per camera per day = 6 Mbps × 86,400 s ÷ 8 (bits→bytes) ÷ 1000 (kB→MB) ÷ 1000 (MB→GB) ≈ **64.8 GB/day**.
- For a 30-day retention requirement: 64.8 × 30 ≈ **1,944 GB (≈1.9 TB) per camera**.
- For a 50-camera site at this profile: 1.9 TB × 50 ≈ **~97 TB** raw, before RAID overhead (typically add 20-40% depending on RAID level) and before accounting for any cameras on a different resolution/fps/retention profile.

**Network bandwidth:** sum sustained bitrates across all cameras simultaneously active on a network segment, add margin for analytics metadata streams and live-viewing client pulls (each operator viewing a stream adds another instance of that camera's bitrate unless multicast is used — see `fundamentals/05-network-design-for-cctv.md`).

**Why this matters for design decisions:** retention period is very often the single biggest lever on cost — a client asking for 90-day retention instead of 30-day triples the storage bill for the same camera count, so this figure needs to be pinned down explicitly at Stage 2 rather than assumed, and the calculation needs to be shown so the client can see the tradeoff.

**Formal reference:** manufacturer bitrate/storage calculators (OEM-published, confirm with OEM per project — the method above is universal, the bitrate figures are not).
