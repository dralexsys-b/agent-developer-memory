# Documents Registry

**Status:** ACTIVE  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Documentation Lead  
**Maintainer:** Documentation Maintainer  

**Type:** Index (Layer 2: Operational Knowledge)  
**Primary Question:** "What documents exist?"  
**Canonical Source for:** Complete registry of project documents  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md  

---

## Registry

| Document | Type | Layer | Lifecycle | Status |
|----------|------|-------|-----------|--------|
| `INFORMATION_ARCHITECTURE.md` | Architecture | 0 (Meta) | Static | ACTIVE |
| `PROJECT_PROTOCOL.md` | Protocol | 1 (Identity) | Static | ACTIVE |
| `DOCUMENTS.md` | Index | 2 (Operational) | Dynamic | ACTIVE |
| `REPOSITORIES.md` | Registry | 2 (Operational) | Semi-static | PLANNED |
| `CURRENT_CONTEXT.md` | Context | 2 (Operational) | Dynamic | ACTIVE |
| `CODE_INDEX.md` | Registry | 2 (Operational) | Dynamic | ACTIVE |
| `RELEASES.md` | History | 2 (Operational) | Dynamic | ACTIVE |
| `ADR_INDEX.md` | Index | 2 (Operational) | Dynamic | PLANNED |
| `ENGINEERING_PLAYBOOK.md` | Playbook | 3 (Engineering) | Semi-static | PLANNED |
| `DOC_STANDARD.md` | Standard | 3 (Engineering) | Static | PLANNED |
| `RELEASE_PROCESS.md` | Playbook | 3 (Engineering) | Semi-static | PLANNED |
| `AUTOMATION.md` | Playbook | 3 (Engineering) | Semi-static | PLANNED |
| `ENGINEERING_HISTORY.md` | History | 3 (Engineering) | Dynamic | PLANNED |


---

## Relationships

**Dependencies:**
- INFORMATION_ARCHITECTURE.md
- PROJECT_PROTOCOL.md

**Dependents:**
- All project documentation

---

## Document Type Definitions

- **Protocol** — defines rules of interaction and responsibilities
- **Standard** — defines requirements for artifacts
- **Playbook** — defines sequence of actions
- **Architecture** — defines system structure
- **Index** — helps find information (navigation)
- **Registry** — authoritative inventory of project entities
- **History** — records past events
- **Context** — describes current state

---

## Layer Definitions

- **Layer 0 (Meta Architecture)** — describes the knowledge system itself
- **Layer 1 (Project Identity)** — defines project identity, roles, principles
- **Layer 2 (Operational Knowledge)** — describes current operational state
- **Layer 3 (Engineering Knowledge)** — defines how the project is developed
- **Layer 4 (Verification Layer)** — immutable artifacts confirming project state

---

## Status Definitions

- **ACTIVE** — document exists and is maintained
- **PLANNED** — document is planned but not yet created
- **ARCHIVED** — document is preserved for historical reference
- **DEPRECATED** — document is superseded by a newer version


---

## End of Document

This document is the canonical registry of project documentation.

All additions, removals, archival, or status changes of project documents must be reflected here.

