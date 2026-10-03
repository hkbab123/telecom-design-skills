# Network Management and OAM

**Why this matters:** a transport network that cannot be seen cannot be maintained; fault location and service visibility drive availability.

## NMS scope

- **Element management (EMS)** — configuration, fault, performance of individual nodes.
- **Network management (NMS)** — end-to-end view across nodes, service provisioning, topology.
- **Service view** — per-service health and path, so operations can tell which subsystem is affected by a fault.

Decide whether the NMS is vendor-supplied per technology layer or a multi-vendor/umbrella system.

## OAM layers

- Physical: optical power monitoring, loss-of-signal.
- Digital transport: SDH/OTN overhead bytes, TCM, error counts.
- Packet: Y.1731 / 802.1ag for connectivity and performance.
- Service: end-to-end tests (loopback, delay, loss).

## Fault management

- Alarm correlation to avoid alarm storms after a cable cut (one fibre break can raise hundreds of downstream alarms).
- Severity classification and escalation rules.
- Integration to the control-room alarm system or enterprise fault manager, defined in an ICD.

## Performance management

Error-performance parameters (ITU-T G.826 for SDH, G.8201 for OTN) and Ethernet metrics: errored seconds, severely errored seconds, delay, loss. Thresholds are set with the client.

## Fibre monitoring

Optional remote fibre test systems monitor spare or live fibres with an OTDR, detecting degradation and localising faults without site visits. Worth the cost on long, high-risk routes.

## Data communication network (DCN)

The management network that reaches every node. Keep it independent of the traffic it manages, with its own redundancy, so a service failure does not cut management access (see `14`).

## Common mistakes

- Using the managed traffic path as the only management path.
- No alarm correlation, leaving operators buried during a fibre cut.
- Not capturing NMS database and configuration backups in the maintenance plan.
