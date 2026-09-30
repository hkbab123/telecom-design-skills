# IP Video Protocols and ONVIF

**ONVIF (Open Network Video Interface Forum)** is the de facto interoperability standard that lets cameras and VMS software from different manufacturers work together. Rather than every VMS needing a custom driver per camera model, ONVIF defines standard "profiles":
- **Profile S** — basic streaming (video/audio transmission, PTZ control) — the baseline almost every IP camera supports.
- **Profile T** — advanced streaming, including H.265 and analytics metadata streaming.
- **Profile G** — storage and recording (edge storage, retrieval).
- **Profile Q** — simplified out-of-the-box configuration and access control.

Specifying "ONVIF Profile S/T conformant" in a tender is what actually protects the client from vendor lock-in — without it, "IP camera" alone says nothing about interoperability.

**Streaming mechanics:** video travels over **RTSP** (Real Time Streaming Protocol, the session-control layer) carrying **RTP** (Real-time Transport Protocol, the actual media packets), typically over UDP for low-latency live viewing or TCP where reliability matters more than latency.

**Codecs:** **H.264** is the mature, universally-supported baseline. **H.265 (HEVC)** roughly halves bitrate for the same quality versus H.264 — directly reduces both network bandwidth and storage cost, at the price of slightly higher camera/VMS processing load and less universal older-hardware support. For a new-build project with modern equipment, H.265 is usually the better default; for a brownfield project integrating with older VMS infrastructure, confirm compatibility first.

**Why this matters for design decisions:** codec choice is a direct input to the bandwidth/storage calculation (`fundamentals/04-bandwidth-storage-calculations.md`) — the same camera count and resolution can produce roughly half the storage bill depending on this one decision, so it belongs early in the Tender-stage sequence, not as an afterthought.

**Formal reference:** ONVIF Profile specifications (onvif.org), ITU-T H.264/H.265 standards, IETF RFC 2326 (RTSP) / RFC 3550 (RTP).
