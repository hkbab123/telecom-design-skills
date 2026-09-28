# Advanced Safety Features — Lone Worker, Man-Down, Geo-Fencing, Ambient Listening

The operational-safety feature layer built on top of standard TETRA call/data mechanics (call-types fundamentals file, 07, and data-services fundamentals file, 08) — read this when the question is "how do these specific personal-safety features actually work," since they're mentioned in Stage 2 item 12's checklist but not designed there in any depth.

## Lone worker — the acknowledgment mechanism

A **lone worker** feature requires a terminal to periodically confirm the user is safe — the terminal (or an app/accessory paired with it) prompts the user at a set interval, and if the user doesn't acknowledge (a button press or equivalent) within a defined response window, the terminal automatically escalates: typically triggering an emergency call/alert to the dispatcher, carrying the terminal's identity and, where GPS-equipped, its last known location. The two parameters that actually define the feature's behaviour, and need to be set deliberately rather than left at a device default:
- **Polling/check-in interval** — how often the terminal prompts the user; too frequent becomes an operational nuisance the user starts ignoring or disabling, too infrequent delays genuine-emergency detection.
- **Acknowledgment response window** — how long the user has to respond before escalation triggers; needs to balance false-alarm risk (a momentary lapse or a user mid-task triggering an unnecessary alert) against genuine-emergency detection speed.

Both parameters are an operational-policy decision for the client to set (informed by the specific work being done — a solitary trackside inspector and a control-room-adjacent worker have different appropriate settings), not a fixed TETRA-standard value, and different terminal/OEM implementations may offer different configurability — confirm what's actually adjustable on the specific terminal model being specified.

## Man-down — the automatic fall/incapacitation detection

A **man-down** alert works differently from lone-worker check-in: rather than requiring an active user acknowledgment, it uses a **tilt-switch or accelerometer-based sensor** (built into the terminal or a paired accessory) that automatically detects if the user has fallen or become horizontal/immobile for an abnormal period, triggering the same kind of emergency escalation without requiring any user action — critical for a scenario where the user is genuinely incapacitated and couldn't acknowledge a lone-worker prompt even if one were sent. The key design/configuration parameters:
- **Tilt-angle threshold** — the angle from vertical that counts as "fallen" (needs tuning to avoid false triggers from normal bending/crouching work postures, which varies by job role — a track worker regularly kneeling has different normal-posture patterns than an office-adjacent worker).
- **Immobility timeout** — how long the abnormal orientation must persist before triggering (distinguishing a genuine fall from a brief stumble that self-corrects).
- **Pre-alert/cancel window** — many implementations give the user a brief window to cancel a triggered alert (in case of a false trigger) before it actually escalates to the dispatcher, avoiding needless emergency responses for sensor false-positives.

As with lone-worker, these thresholds are configuration parameters to tune with the client against their specific work environment and posture patterns, not universal defaults — and, like lone-worker, this is a terminal/accessory hardware capability that varies by OEM and model, so availability and configurability should be confirmed against the specific terminal being specified, not assumed present on every TETRA handheld.

## Geo-fencing — location-triggered behaviour changes

**Geo-fencing** uses the same GPS-location-reporting mechanism (data-services fundamentals file, 08) to automatically change a terminal's behaviour when it crosses a defined virtual boundary — the two most common applications relevant to rail/O&G:
- **Automatic talkgroup switching** — a terminal automatically switches to a different talkgroup when entering a specific zone (e.g. a worker's radio switches to the "confined space entry" talkgroup on entering a permit-required area, or a train's onboard radio switches to a station-specific talkgroup on entering a station's zone) — reducing the risk of a user forgetting to manually switch groups at exactly the moment it matters.
- **Zone-entry alerting** — a notification (to the dispatcher, or back to the user) when a terminal enters or exits a defined hazardous or restricted zone, independent of any talkgroup change.

Geo-fencing depends on the terminal's GPS accuracy and reporting frequency (interacting directly with the control-channel-loading consideration in the data-services fundamentals file) and on the dispatcher/management platform's capability to define and enforce zone boundaries — again a genuinely OEM/platform-specific capability, not a standard TETRA air-interface feature, so its availability should be confirmed with the specific chosen platform rather than assumed generic.

## Ambient listening — the operational-policy-sensitive feature

Briefly named in Stage 2 item 12: **ambient listening** lets a dispatcher remotely and discreetly open a terminal's microphone without an audible indication to the user, used to assess an unfolding situation (a hijacking, an active security breach, a worker who's triggered an emergency alert but isn't responding to voice calls) where a normal call would either alert a threat actor or simply not be answerable. This is the single most operationally and legally sensitive feature in this file: because it covertly captures audio without the user's active participation, its use is typically governed by strict internal authorisation policy (who can trigger it, under what documented circumstances) and, in many jurisdictions, specific legal constraints on covert audio surveillance of employees — the technical capability (an OEM platform feature, confirmed available on the chosen dispatcher platform) is the easy part; the authorisation policy and legal-compliance sign-off is the part that actually needs to be resolved with the client's legal/compliance function before the feature is enabled operationally, not treated as a routine configuration toggle.

## Why this matters for design decisions

- Lone-worker and man-down are terminal/accessory hardware capabilities that vary by OEM and model — confirm availability and configurable-parameter range on the specific terminal being specified before promising the feature in a technical specification, and capture the client's actual threshold/interval requirements as explicit inputs rather than device defaults.
- Geo-fencing capability (automatic talkgroup switching, zone alerting) is a dispatcher/management-platform feature, not a universal TETRA capability — confirm what the specific OEM's platform actually supports during vendor evaluation.
- Ambient listening should never be treated as "just another dispatcher function" in a technical specification — flag it explicitly for the client's legal/compliance function to set an authorisation policy around, alongside confirming the technical capability itself.

Formal reference: no ETSI TETRA standard defines these specific feature behaviours in detail — they're OEM platform/terminal capabilities built on top of the standard call-control (EN 300 392-2) and SDS/data (EN 300 392-2/392-3) mechanisms, so exact behaviour and configurability are genuinely vendor-specific throughout.
