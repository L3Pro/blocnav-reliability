# BlocNav – Reliability Notes

This repository documents reliability principles, failure modes, and operational lessons discovered while building **BlocNav**, an offline-first mapping system designed for real-world field conditions.

Most mapping systems assume:
- stable connectivity
- low latency
- static data
- ideal usage environments

BlocNav is built from the opposite assumption:
**connectivity is unreliable, slow networks are deceptive, and field conditions are hostile to happy-path design.**

This repository exists to:
- document non-obvious failure modes observed during real field testing
- make design principles explicit and inspectable
- preserve operational lessons before they are forgotten
- provide context for pilots, partners, and evaluators

This is **not** a source-code repository.
No implementation details, schemas, or infrastructure configurations are published here.

The canonical BlocNav application codebase remains private.

## Contents

- `DESIGN_PRINCIPLES.md` – non-negotiable system rules inferred from field experience
- `FAILURE_MODES.md` – real ways maps fail outside ideal conditions
- `PILOT_SCOPE.md` – what BlocNav currently supports and intentionally excludes

This repository favors clarity over completeness.
It is expected to grow slowly.
