# Design Principles

These principles describe non-negotiable rules enforced by the BlocNav system.
They are derived from real field use and observed failure modes, not aspiration or preference.

The purpose of these principles is alignment and constraint.
They exist to reduce ambiguity in design decisions and prioritize correctness under non-ideal conditions.

---

## Principle: Offline Is Canonical

If local data exists, the system must render and function without waiting for network access.

Connectivity may enhance the system, but it must never be required for core operation.
Local state is treated as the source of truth.

---

## Principle: Slow Online Is Worse Than Offline

A weak or degraded network is a failure state, not a success state.

The system must not prioritize network requests simply because connectivity is technically present.
When online conditions are poor, the system should favor local data and deterministic behavior over delayed or blocking operations.

---

## Principle: Local Persistence Before Sync

Data capture must succeed locally before any attempt to synchronize with a remote system.

If data is not safely stored on the device, it is considered lost.
Synchronization failures are acceptable; capture failures are not.

---

## Principle: Capture Now, Structure Later

During field use, speed and safety take precedence over structure and completeness.

The system must minimize cognitive load at the moment of capture.
Validation, enrichment, and classification are deferred to later stages when conditions allow.

---

## Principle: Silence Beats Lying

It is better to show nothing than to show something incorrect or misleading.

The system should avoid spinners, false progress indicators, or optimistic assumptions when certainty does not exist.
User trust is preserved through restraint, not reassurance.

---

## Principle: Operational Continuity First

Operational continuity takes precedence over synchronization, freshness, or completeness.

The system must remain usable and predictable regardless of connectivity state. Loss of network access must never prevent map rendering, observation capture, or local state access.

A stale but available map is preferable to a fresh but unavailable map.

Synchronization improves shared awareness but must never be required for individual operational continuity.

Continuity is the primary invariant.

---

## Principle: Network Independence

Connectivity is an enhancement, not a dependency.

All critical operations — including map rendering, observation capture, and state persistence — must function correctly without network access.

Network availability must only affect synchronization and external data retrieval, never core system usability.

Connectivity loss is a normal operating condition and must be handled predictably.

---

## Principle: Immediate Local Persistence

All user actions that create or modify operational data must be persisted locally immediately and durably.

Data must never be held only in volatile memory or pending network transmission.

Persistence must occur before any attempt at synchronization.

Synchronization failure must never result in data loss.

Local durability is the first guarantee. Synchronization is the second.

---

## Principle: Device Autonomy

Each device must be capable of operating as a durable, independent system node.

Devices must retain sufficient local state to:

- render previously accessed maps
- display previously captured observations
- capture new observations
- preserve operational continuity

Devices must never assume cloud availability to maintain operational correctness.

Cloud infrastructure improves coordination but must not be required for system survival.

---

## Principle: Explicit Degraded Network Handling

Degraded connectivity (high latency, stalled responses, intermittent packet loss) must be detected and handled explicitly.

Partial connectivity is more dangerous than complete disconnection because it creates false confidence in system functionality.

The system must fail predictably and visibly under degraded network conditions rather than silently stall or block.

When degraded conditions are detected, the system must prioritize local state, cached data, and predictable behavior.

---

## Principle: Capture Reliability Over Synchronization

Observation capture must succeed regardless of network state.

The system must always allow users to record observations, with guaranteed local persistence.

Synchronization must occur opportunistically and asynchronously.

Capture reliability must never be coupled to network availability.

Operational record integrity takes precedence over immediate shared visibility.

---

