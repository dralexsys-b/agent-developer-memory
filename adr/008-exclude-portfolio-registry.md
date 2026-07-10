# ADR 008: Exclude Program Portfolio and Program Registry from Program Recovery

**Date:** 2026-07-09
**Status:** ACCEPTED
**Authority:** Engineering Lead
**Context:** Program Recovery v1 originally included Commit 10 (Program Portfolio) and Commit 11 (Program Registry). During execution, it became clear that these are not required for the current phase.

## Decision
Exclude Commit 10 (Program Portfolio) and Commit 11 (Program Registry) from Program Recovery v1.

## Rationale
- Portfolio is a higher-level management concept not needed for current project scale (only a handful of programs).
- Registry is an implementation detail of PROGRAMS.md, not a separate governance concept.
- Keeping these commits would add unnecessary complexity without immediate benefit.
- The project's current phase focuses on establishing foundational program management, not advanced portfolio management.

## Impact
- Program Recovery v1 is reduced from 20 to 18 commits (removing Commit 10–11).
- PROGRAMS.md will be created in Phase 2 without a separate Registry document.
- The decision is documented to prevent future confusion.

## Alternatives Considered
1. Keep both commits — rejected due to over-engineering.
2. Merge Portfolio and Registry into PROGRAMS.md — accepted as the chosen approach.

## Related Documents
- PROGRAM_MANAGEMENT.md — defines the program management framework.
- PROGRAMS.md — will contain the program registry directly.
