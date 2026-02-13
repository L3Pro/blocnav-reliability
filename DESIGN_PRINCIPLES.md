# Design Principles

These principles are invariants enforced by the BlocNav system.

They are derived from real field use and observed failure modes, not aspiration or preference.

They exist to constrain design decisions, eliminate ambiguity, and preserve operational reliability under degraded or hostile conditions.

These are not guidelines or best practices. They are enforced system properties.

If a proposed change violates these principles, the change must be rejected or redesigned.

---

## Principle: Operational Continuity Is Primary

The system must remain usable and predictable regardless of connectivity state.

Loss of network access must never prevent:

- map rendering from available local data
- observation capture
- access to previously stored state

A stale but available map is preferable to a fresh but unavailable map.

Continuity is the primary invariant. Synchronization is secondary.

---

## Principle: Offline State Is Authoritative for Immediate Operation

If local data exists, the system must render and function without waiting for network access.

Connectivity may enhance the system, but it must never be required for core operation.

Local state is authoritative for immediate operational correctness.

Cloud state improves coordination, not device viability.

---

## Principle: Device Autonomy

Each device must function as a durable, independent system node.

Devices must retain sufficient local state to:

- render previously accessed maps
- display previously captured observations
- capture and persist new observations
- maintain operational continuity without cloud access

Devices must never assume network or server availability to operate correctly.

---

## Principle: Local Persistence Before Synchronization

All operational data must be persisted locally and durably before any attempt to synchronize.

If data is not safely stored on the device, it is considered lost.

Synchronization failures are acceptable. Persistence failures are not.

Local durability is the first guarantee. Synchronization is the second.

---

## Principle: Capture Reliability Over Synchronization

Observation capture must succeed regardless of network state.

The system must always allow users to record observations with guaranteed local persistence.

Synchronization must occur opportunistically and asynchronously.

Capture reliability must never depend on connectivity.

Operational record integrity takes precedence over immediate shared visibility.

---

## Principle: Never Block on Uncertain State

The system must not block core user actions while waiting for network responses or external confirmation.

If certainty cannot be achieved immediately, the system must proceed using the best available local state.

Blocking behavior introduces operational fragility and undermines reliability.

Progress must always be possible using deterministic local information.

---

## Principle: Degraded Connectivity Is a Failure State

Weak, slow, or intermittent connectivity is a failure condition, not a success condition.

The system must not prioritize network operations simply because connectivity technically exists.

When degraded connectivity is detected, the system must favor local state, cached data, and deterministic behavior.

Partial connectivity is more dangerous than complete disconnection because it creates false confidence in system functionality.

---

## Principle: Explicit Handling of Network Degradation

Degraded network conditions must be detected and handled explicitly.

The system must fail predictably and visibly rather than silently stall, block, or mislead the user.

Connectivity loss is a normal operating condition, not an exceptional state.

Connectivity affects synchronization only, never core system usability.

---

## Principle: Silence Is Preferable to Incorrectness

The system must never display incorrect, speculative, or misleading information.

When certainty does not exist, the system must prefer absence of information over false reassurance.

Spinners, optimistic progress indicators, and speculative UI states must not imply correctness where none exists.

User trust is preserved through correctness, not reassurance.

---

## Principle: Capture Must Minimize Cognitive and Operational Load

During field use, speed, safety, and reliability take precedence over structure and completeness.

The system must minimize required input and cognitive burden at the moment of capture.

Validation, enrichment, and structural refinement must be deferred to later stages when conditions allow.

Capture must remain reliable under stress, motion, and degraded conditions.

---

