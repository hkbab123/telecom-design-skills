# Train-Borne CCTV and VRS

**VRS (Video Recording System)** is the standard transit-industry term for the onboard train CCTV/recording subsystem — distinct from trackside/station CCTV, and usually specified and procured separately (often as part of the rolling-stock contract rather than the trackside telecom contract), though the two must interface.

**Driver's forward-facing camera.** A safety- and incident-investigation-relevant camera recording the driver's view ahead — used for incident reconstruction (signal passed at danger, level-crossing incidents, obstruction strikes). Distinct in purpose from passenger-saloon CCTV and typically has its own retention/protection requirement (often longer retention, restricted access, tied to incident-investigation regulation).

**Passenger-saloon CCTV.** Standard deterrence/evidentiary coverage inside each carriage — design constraints here are more about vibration, power-supply stability (onboard DC power systems, not mains), and vandalism-resistant housings than about the tunnel-specific EMC concerns of trackside cameras.

**Onboard-to-trackside offload.** Recorded footage on a moving train has to reach the central VMS somehow — common patterns are (a) continuous wireless offload via trackside WiFi/cellular at stations or depots where the train dwells long enough, or (b) physical media/local extraction at the depot, with only live-view (not continuous recording) streamed wirelessly while in service, if at all. Bandwidth and dwell-time constraints usually rule out real-time continuous streaming of full-resolution footage from every train — this needs to be explicitly decided, not assumed.

**Why this matters for design decisions:** VRS sits at a genuine interface boundary between the rolling-stock supplier and the trackside/station CCTV contractor — the ICD between them (who owns the onboard-to-trackside handover point, what format/protocol, what triggers an offload) is one of the more commonly under-specified interfaces on a rail project, so flag it explicitly rather than assuming it falls naturally to one party.

**Formal reference:** no single unifying international standard — VRS specifications are typically set by the rolling-stock procurement specification and/or the transit authority's own onboard-CCTV standard; confirm the applicable requirement per project rather than assuming IEC 62676 alone covers onboard systems.
