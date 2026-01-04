# Design Principles

These principles describe non-negotiable rules enforced by the BlocNav system.
They are derived from real field use and observed failure modes, not aspiration or preference.

The purpose of these principles is alignment and constraint.
They exist to reduce ambiguity in design decisions and prioritize correctness under non-ideal conditions.

---

## Offline Is Canonical

If local data exists, the system must render and function without waiting for network access.

Connectivity may enhance the system, but it must never be required for core operation.
Local state is treated as the source of truth.

---

## Slow Online Is Worse Than Offline

A weak or degraded network is a failure state, not a success state.

The system must not prioritize network requests simply because connectivity is technically present.
When online conditions are poor, the system should favor local data and deterministic behavior over delayed or blocking operations.

---

## Local Persistence Before Sync

Data capture must succeed locally before any attempt to synchronize with a remote system.

If data is not safely stored on the device, it is considered lost.
Synchronization failures are acceptable; capture failures are not.

---

## Capture Now, Structure Later

During field use, speed and safety take precedence over structure and completeness.

The system must minimize cognitive load at the moment of capture.
Validation, enrichment, and classification are deferred to later stages when conditions allow.

---

## Silence Beats Lying

It is better to show nothing than to show something incorrect or misleading.

The system should avoid spinners, false progress indicators, or optimistic assumptions when certainty does not exist.
User trust is preserved through restraint, not reassurance.
