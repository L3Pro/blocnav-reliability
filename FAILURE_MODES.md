# Failure Modes

This document records real, observed ways mapping systems fail in non-ideal field conditions.

These are not hypothetical edge cases. They are empirically observed failure modes encountered through live use and field testing.

The purpose of this document is to ensure these failure modes are permanently understood and prevented.

---

## Failure Mode: Deceptive Connectivity (Slow Networks Are Worse Than Offline)

### Definition

A failure mode where network connectivity technically exists, but is too slow, high-latency, or unstable to support reliable operation.

The system detects "online" status and prioritizes network requests, even though usable local data is already present.

This causes the system to behave worse than if it had assumed offline state.

---

### Observed Symptoms

- Blank or partially rendered maps despite cached tiles or local data being present
- Long-loading spinners with no visible progress
- POIs or layers failing to appear until network timeouts complete
- Delayed or blocked UI responsiveness during marginal connectivity
- Immediate system improvement when device is switched to airplane mode

---

### Root Cause

Most systems treat connectivity as a binary state: online or offline.

When `navigator.onLine === true`, systems assume network access is viable and prioritize network requests.

In degraded conditions such as:

- high latency
- packet loss
- low bandwidth
- unstable connections

network requests stall, block, or delay rendering.

Local cached data exists but is not used immediately because the system defers to network retrieval.

This introduces unnecessary blocking and reduces system usability.

---

### Why Typical Systems Fail Here

Typical cloud-first architectures assume:

- network access is reliable
- network latency is acceptable
- online state implies usable connectivity

These assumptions break in real field environments.

The system defers to cloud state even when local state is sufficient.

This violates operational continuity.

---

### Operational Impact

This failure mode creates severe operational risk:

- System appears non-functional despite having usable local data
- Users lose trust in system reliability
- Critical situational awareness may be temporarily unavailable
- Users may abandon the system or revert to unsafe alternatives
- Operational continuity is compromised

This failure mode is common during:

- highway travel through marginal coverage zones
- disaster response with congested cellular infrastructure
- rural and remote operations
- dense urban environments with intermittent signal reflection or handoff

---

### Detection Signals

This failure mode can be detected when:

- Network requests exceed acceptable latency thresholds
- Tile or data requests stall without progress
- Cached data exists but rendering is delayed pending network response
- Connectivity state rapidly oscillates between usable and unusable

Binary online/offline detection is insufficient.

Connectivity quality must be inferred from actual request performance.

---

### Required System Behavior

The system must prioritize deterministic local state over uncertain network state.

Specifically:

- Local cached tiles must render immediately if present
- Local POIs and operational data must render immediately if present
- Network requests must never block rendering of available local data
- Network requests must be opportunistic and asynchronous
- The system must degrade gracefully to local-only operation

The system must behave as offline-first, even when technically online.

---

### Prevention Invariant

Local operational continuity must never depend on network request success.

Network availability may improve system completeness, but must never determine system usability.

If local data exists, it must be rendered immediately and deterministically.

Connectivity state must not override local state availability.

---

### BlocNav Design Response

BlocNav explicitly enforces the following protections:

- Cache-first rendering for tiles and operational layers
- Immediate rendering of locally persisted POIs and observations
- Non-blocking synchronization architecture
- Asynchronous, opportunistic network requests
- Explicit degraded-network handling logic

This ensures degraded connectivity cannot block operational continuity.

