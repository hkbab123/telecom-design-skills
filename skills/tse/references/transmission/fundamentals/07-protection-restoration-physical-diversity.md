# Protection, Restoration and Physical Diversity

**Technical basis for Rule 1:** physical diversity is not logical diversity.

## Protection vs restoration

- **Protection** — pre-planned, pre-provisioned alternate path; switches in tens of milliseconds.
- **Restoration** — alternate path computed after failure; slower (seconds or more); needs spare capacity and a control plane.

Operational services (control, voice alarm, radio backhaul) generally need protection; best-effort services may accept restoration.

## Common schemes

| Scheme | Description |
|---|---|
| 1+1 | Traffic sent on both paths; receiver selects the better; fastest, uses 2× capacity |
| 1:1 | Traffic on working path; protection path idle or carries low-priority traffic |
| Ring (SNCP, MS-SPRing, ERPS) | Traffic routed the other way around the ring after a break |
| Dual-homing | A site is connected to two different aggregation nodes |

## The SRLG problem

A **shared-risk link group** is a set of links that fail together because they share a physical element: a duct, trench, bridge, tunnel segment, cross-passage, cable tray, or even a power feed or joint chamber. Examples:

- Rail ring built in a single tunnel: both "directions" of the ring run along the same wall; a derailment, fire or cable-tray collapse cuts both.
- Two cables in the same duct, or in adjacent ducts crossing the same bridge.
- O&G pipeline-corridor "ring" where the return leg follows the same corridor.

### How to check

1. Draw the **physical** route for each protected path on the survey base (not the logical topology).
2. List every shared structure; record it in an **SRLG register** (route section, shared element, affected paths, consequence).
3. For each entry choose: re-route, separate to a different physical structure, accept with client sign-off, or add a third path.
4. Re-check after any civil-design change.

## Multiple failures

Specify behaviour for double failures (e.g. cut during a planned maintenance). A ring tolerates one cut; two cuts partition it. Decide which services must still run in each partition (see `09`).

## Switch time

Typical target is ≤50 ms for many operational services (illustrative); some applications tolerate more. Verify actual switch time in FAT/SAT with real fault simulation (see `15`).

## Common mistakes

- Presenting a ring as "fully protected" without a physical-route check.
- Counting a tunnel-wall tray as two separate routes.
- Forgetting that node power or a shared patch panel is also a single point of failure.
