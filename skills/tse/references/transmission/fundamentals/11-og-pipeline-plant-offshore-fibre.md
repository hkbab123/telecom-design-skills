# O&G: Pipeline Corridor, Plant Rings and Offshore Fibre

**Why this matters:** O&G fibre runs through long, remote corridors and classified areas, with different failure modes from rail.

## Pipeline-corridor backbone

- Cable is typically buried in the same right-of-way as the pipeline, giving long, unsupervised routes.
- Main hazards: third-party excavation (the leading cause of cuts), corrosion/cathodic-protection interactions with metallic armour, flooding, rodent damage.
- Mitigation: warning tape and markers, route patrols, burial depth per client standard, non-metallic or properly earthed armoured cable per the project's cathodic-protection design.
- Ring closure often needs a **different** corridor; a return leg beside the same pipeline is an SRLG (see `07`).

## Plant and terminal rings

- Rings through process areas combine long cable runs, many junction boxes and hazardous zones.
- Keep fibre in segregated routes from power and high-voltage cable; use duct banks and marked underground routes.
- Node locations (field auxiliary rooms/instrument rooms) are typically in safe areas; field devices in zoned areas connect through certified equipment or barriers.

## Hazardous-area optical power

Optical radiation can ignite an explosive atmosphere if power is high enough. IEC 60079-28 sets limits and protection concepts. Standard transceivers usually sit well below limits, but amplified DWDM systems and high-power lasers need explicit assessment when light can be emitted into a classified area (open connector, damaged fibre). Confirm with the OEM and the project's hazardous-area authority; do not assume.

Fibre cable itself is non-conductive, but armour, tracer wires and cable entries need appropriate certified glands and bonding where they enter Ex areas.

## Offshore and subsea (short links)

- Platform-to-platform and platform-to-shore links use subsea armoured cable; repair needs vessels and weather windows, so MTTR is measured in days to weeks.
- Always consider diversity or an alternate medium (microwave, satellite) for critical services, as the cable is an SRLG per landing.
- Long-haul repeatered subsea systems are out of scope.

## Telemetry and sensing

Fibre can also serve distributed sensing (temperature, acoustic) along pipelines. That is a separate system and is noted as a thin item; interface and shared-fibre rules matter if it shares cable with telecom (see `16`).

## Common mistakes

- Planning a "ring" along one pipeline corridor.
- Ignoring optical-power assessment for amplified links into classified areas.
- Underestimating offshore repair time in the availability model.
