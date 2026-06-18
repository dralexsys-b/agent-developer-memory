# Repositories Registry

**Status:** ACTIVE  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Infrastructure Lead  
**Maintainer:** Infrastructure Maintainer  

**Type:** Registry (Layer 2: Operational Knowledge)  
**Primary Question:** "Where is the code?"  
**Canonical Source for:** Complete registry of project repositories  

---

## Relationships

**Dependencies:**
- INFORMATION_ARCHITECTURE.md
- PROJECT_PROTOCOL.md

**Dependents:**
- CODE_INDEX.md
- CURRENT_CONTEXT.md
- DOCUMENTS.md

---

## Registry

| Repository | Purpose | URL | Default Branch | Baseline | Owner | Status |
|------------|---------|-----|----------------|----------|-------|--------|
| `agent-developer-runtime` | Source code, orchestrators, tools | https://github.com/dralexsys-b/agent-developer-runtime | main | agent-dev-v0.2.0-r1 | Infrastructure Lead | ACTIVE |
| `agent-developer-memory` | Documentation, ADR, evidence, protocols | https://github.com/dralexsys-b/agent-developer-memory | main | agent-dev-v0.2.0-r1 | Documentation Lead | ACTIVE |


---

## Repository Layout

### agent-developer-memory

**Key directories:**
- `evidence/` — immutable verification artifacts (logs, test results, benchmarks)
- `adr/` — architecture decision records (future)

**Note:** Repository layout is defined here. Detailed file inventory is maintained in `CODE_INDEX.md`.

### agent-developer-runtime

**Key directories:**
- `src/` — source code (orchestrators, tools)
- `tests/` — test files (future)

**Note:** Repository layout is defined here. Detailed file inventory is maintained in `CODE_INDEX.md`.

---

## Repository Rules

1. **Runtime Repository** contains only executable code and runtime artifacts
2. **Memory Repository** contains only documentation, protocols, and evidence
3. Evidence files are immutable and never modified after creation
4. Documentation follows the structure defined in INFORMATION_ARCHITECTURE.md
5. All changes to repositories require evidence (logs, test results)


---

## Status Definitions

- **ACTIVE** — repository is actively maintained
- **ARCHIVED** — repository is preserved but no longer actively developed
- **DEPRECATED** — repository is superseded by a newer repository

---

## End of Document

This document is the canonical registry of project repositories.

All additions, removals, or status changes of project repositories must be reflected here.

