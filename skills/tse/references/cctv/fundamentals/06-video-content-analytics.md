# Video Content Analytics (VCA)

VCA runs algorithms against the video stream (either at the camera edge or centrally at the VMS) to generate operator alerts or metadata, without a human watching every screen continuously. Common types:

- **Motion detection** — the most basic; triggers on pixel change within a defined zone. High false-alarm rate in outdoor/variable-lighting conditions (moving shadows, weather, wildlife) unless tuned carefully.
- **Line-crossing / intrusion-zone detection** — triggers when an object crosses a defined virtual line or enters a defined zone — the core perimeter-security analytic.
- **Loitering detection** — triggers when an object remains in a zone beyond a set time threshold.
- **ANPR (Automatic Number Plate Recognition)** — reads vehicle plates, common at rail depot/yard access points and O&G site entry control.
- **PPE detection** — increasingly used in O&G for compliance monitoring (hard-hat, hi-vis detection in defined zones).

**False-alarm-rate management** is the practical bottleneck for every analytic above — an analytic that fires constantly on irrelevant triggers gets ignored by operators (alarm fatigue, the same underlying problem SCADA's EEMUA 191 alarm-rationalisation addresses for process alarms). Tuning zone definitions, sensitivity thresholds, and time-of-day/lighting-condition adjustment is real design work, not a one-time camera-install setting.

**Why this matters for design decisions:** VCA is the layer where the detection-vs-verification boundary (rule 1, `fundamentals/07-cctv-as-verification-not-detection.md`) gets tested in practice — a VCA alert can support an operator's decision, but treating it as equivalent to a certified detection-system alarm is the mistake this skill exists to prevent.

**Formal reference:** no single governing standard for VCA algorithm performance — manufacturer-published detection/false-alarm-rate specifications (confirm with OEM), evaluated against the project's own acceptance-testing criteria at FAT/SAT.
