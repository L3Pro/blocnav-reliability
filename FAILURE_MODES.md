# Failure Modes

This document records real, observed ways mapping systems fail in non-ideal field conditions.
These are not hypothetical edge cases; they are failure modes encountered through live use and testing.

---

## Deceptive Connectivity (Slow Networks Are Worse Than Offline)

### Definition
A failure mode where a network connection technically exists, but is too slow, high-latency, or unstable to be usable.
The system detects “online” status and attempts network requests, blocking or delaying access to local data that is already available.

### Symptoms
- Blank or partially rendered maps despite cached tiles or data being present
- Long-loading spinners with no visible progress
- POIs and layers failing to appear until the network request times out
- System behavior improves immediately when the device is placed in airplane mode

### Why Typical Systems Fail Here
Most applications treat connectivity as a binary state: online or offline.
When `online === true`, network requests are prioritized by default.

In degraded network conditions (e.g. low bandwidth, high latency, packet loss):
- Online requests stall or block rendering
- Local caches are bypassed or deferred
- The user experiences a worse outcome than if the system had assumed offline state

This creates a paradoxical condition where **having a weak network is more damaging than having no network at all**.

### Operational Impact
In field environments, this failure mode:
- Creates the appearance of system failure when local data is actually intact
- Erodes user trust (“the map doesn’t work here”)
- Encourages unsafe workarounds or repeated retries
- Masks the reliability of offline-capable systems

This failure mode is especially common during:
- highway travel through marginal coverage zones
- disaster events with congested cellular networks
- rural or remote operations with intermittent signal
