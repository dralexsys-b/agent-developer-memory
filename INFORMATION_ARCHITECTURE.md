# Information Architecture

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Project Architect  
**Maintainer:** Project Maintainer  

This document defines the information architecture of the Agent Developer project.  
It stands ABOVE the ADR system and is not itself an ADR.  
It defines the structure in which all other documentation lives.

---

## Scope

This document defines:
- How project knowledge is organized
- What documents exist and why
- How information flows between layers
- What invariants must be preserved
- Who has authority and who maintains what

This document does NOT define:
- Runtime architecture
- Software architecture
- Implementation details
- Engineering procedures
- Specific ADRs

---

## Dependencies

**Dependencies:** None  
**Dependents:** All documentation

This document is the absolute root of the knowledge tree.  
It has no external dependencies.  
All other documents depend on it.

---

## Document Lifecycle Rules

This document may only be:
- Clarified
- Extended
- Deprecated
- Amended via appendix

This document may NOT be:
- Completely rewritten

If a fundamental change to the information architecture is required,  
create `INFORMATION_ARCHITECTURE_V2.md` and archive this version.


## Information Model

The project knowledge is organized into five layers:

### Layer 0: Meta Architecture

**Purpose:** Describes the knowledge system itself.  
**Documents:** INFORMATION_ARCHITECTURE.md  
**Question answered:** "How is knowledge organized?"  
**Lifecycle:** Static  
**Update frequency:** Extremely rare (only when fundamental restructuring is needed)

---

### Layer 1: Project Identity

**Purpose:** Defines the project's identity, roles, principles, and structure.  
**Documents:** PROJECT_PROTOCOL.md  
**Question answered:** "What is this project?"  
**Lifecycle:** Static  
**Update frequency:** Rare (only when roles, principles, or structure change)

---

### Layer 2: Operational Knowledge

**Purpose:** Describes the current operational state of the project.  
**Documents:**
- CURRENT_CONTEXT.md (Planned document)
- CODE_INDEX.md (Exists)
- RELEASES.md (Exists)
- ADR_INDEX.md (Planned document)
- DOCUMENTS.md (Planned document)
- REPOSITORIES.md (Planned document)

**Question answered:** "What is the current state of the project?"  
**Lifecycle:** Dynamic  
**Update frequency:** Constant (changes with every milestone, release, or file addition)

---

### Layer 3: Engineering Knowledge

**Purpose:** Defines how the project is developed, released, and maintained.  
**Documents:**
- ENGINEERING_PLAYBOOK.md (Planned document)
- DOC_STANDARD.md (Planned document)
- RELEASE_PROCESS.md (Planned document)
- AUTOMATION.md (Planned document)
- ENGINEERING_HISTORY.md (Planned document)

**Question answered:** "How do we develop this project?"  
**Lifecycle:** Semi-static  
**Update frequency:** Occasional (changes when processes evolve)

---

### Layer 4: Verification Layer

**Purpose:** Contains immutable artifacts that confirm project state, behavior, quality, performance, or reproducibility.  
**Documents:**
- evidence/ (Exists)
- logs/ (Future directory)
- benchmarks/ (Future directory)
- reports/ (Future directory)

**Question answered:** "What proof do we have?"  
**Lifecycle:** Immutable  
**Update frequency:** Created once, never modified


## Knowledge Lifecycle

Every document belongs to one of four lifecycle categories:

### Static

**Definition:** Documents that almost never change.  
**Characteristics:**
- Define fundamental principles and structures
- Changes require architectural review
- Serve as stable foundation for other documents

**Examples:**
- PROJECT_PROTOCOL.md
- ENGINEERING_PLAYBOOK.md
- DOC_STANDARD.md

---

### Semi-static

**Definition:** Documents that change occasionally.  
**Characteristics:**
- Define processes and procedures
- Changes occur when processes evolve
- Updates are planned and documented

**Examples:**
- RELEASE_PROCESS.md
- AUTOMATION.md

---

### Dynamic

**Definition:** Documents that change constantly.  
**Characteristics:**
- Reflect current operational state
- Updated frequently as project evolves
- Represent "living" knowledge

**Examples:**
- CURRENT_CONTEXT.md
- RELEASES.md
- ENGINEERING_HISTORY.md
- CODE_INDEX.md

---

### Immutable

**Definition:** Artifacts created once and never modified.  
**Characteristics:**
- Serve as historical evidence
- Cannot be edited after creation
- If correction is needed, create new artifact with explanation

**Examples:**
- evidence/ (logs, benchmarks, reports)
- ADR files (changes via new ADR or status update)


## Document Types

Every document in the project belongs to one of the following types:

| Type | Purpose | Example |
|---|---|---|
| **Protocol** | Defines rules of interaction and responsibilities | PROJECT_PROTOCOL.md |
| **Standard** | Defines requirements for artifacts | DOC_STANDARD.md |
| **Playbook** | Defines sequence of actions | ENGINEERING_PLAYBOOK.md |
| **Architecture** | Defines system structure | INFORMATION_ARCHITECTURE.md |
| **Index** | Helps find information (navigation) | ADR_INDEX.md, DOCUMENTS.md |
| **Registry** | Defines an authoritative inventory of project entities | REPOSITORIES.md, CODE_INDEX.md |
| **History** | Records past events | ENGINEERING_HISTORY.md |
| **Context** | Describes current state | CURRENT_CONTEXT.md |

### Distinction: Index vs Registry

**Index** helps navigate to information. It answers "Where can I find X?"  
**Registry** is an authoritative inventory. It answers "What entities exist?"

Example:
- DOCUMENTS.md is an **Index** (helps find documents)
- REPOSITORIES.md is a **Registry** (official list of repositories)
- CODE_INDEX.md is a **Registry** (official list of code files)

When creating a new document, first determine its type, then assign a name.

---

## Document Contracts

Every document must have a contract that defines:

1. **Primary Question:** What single question does this document answer?
2. **Purpose:** Why does this document exist?
3. **Canonical Source:** What facts does this document own?
4. **Dependencies:** What other documents does it reference?
5. **Dependents:** What documents reference it?
6. **Lifecycle:** Static / Semi-static / Dynamic / Immutable

### Canonical Source Concept

**Definition:** The unique document that owns a specific fact.

**Rule:** Every fact has exactly one Canonical Source.

**Example:**
- Current milestone → Canonical Source: CURRENT_CONTEXT.md
- List of files → Canonical Source: CODE_INDEX.md
- Release history → Canonical Source: RELEASES.md
- Engineering principles → Canonical Source: PROJECT_PROTOCOL.md

Other documents may **reference** these facts, but never **duplicate** them.


## Information Flows

Information flows through the system in specific patterns. These flows are not dependencies between documents, but rather the movement of knowledge from creation to consumption.

### Primary Pipeline

The main flow of information follows this path:

    Implementation
        ↓
    Evidence (Layer 4)
        ↓
    Validation
        ↓
    Operational State (Layer 2)
        ↓
    Engineer consumes knowledge

**Description:**
1. Developer implements changes (Layer 3: Engineering Knowledge)
2. Evidence is generated (Layer 4: Verification Layer)
3. Evidence is validated against acceptance criteria
4. Operational state is updated (Layer 2: Operational Knowledge)
5. Engineer reads current state to understand project

---

### Parallel Flows

Multiple information flows operate simultaneously:

#### Architecture Decision Flow

    Architecture Decision
        ↓
    ADR-* (created)
        ↓
    ADR_INDEX (updated)
        ↓
    Engineer references decision

#### Engineering Process Flow

    Engineering Knowledge
        ↓
    ENGINEERING_PLAYBOOK
        ↓
    Developer follows procedures

#### Release Process Flow

    Release Process
        ↓
    RELEASE_PROCESS
        ↓
    Release Manager executes release

#### Historical Knowledge Flow

    Lessons Learned
        ↓
    ENGINEERING_HISTORY
        ↓
    Engineer studies past decisions

---

### Flow Direction Rule

**Authority flows downward.**  
**Information may flow upward only as evidence.**

- Layer 0 (Meta Architecture) defines rules for all lower layers
- Layer 1 (Project Identity) defines rules for Layers 2-4
- Layer 2 (Operational Knowledge) reflects current state
- Layer 3 (Engineering Knowledge) defines procedures
- Layer 4 (Verification Layer) provides evidence

Lower layers cannot redefine higher-layer concepts. They can only provide evidence that may inform higher-layer decisions.


## Information Invariants

The following 12 invariants must be preserved at all times. Violation of any invariant indicates an architectural error that must be corrected before proceeding.

### Invariant 1: Single Canonical Source

Every fact has exactly one Canonical Source.  
No document may duplicate facts owned by another document.

### Invariant 2: No Duplication

Documents never duplicate facts.  
They may reference facts, but never copy them.

### Invariant 3: Evidence Immutability

Evidence is never edited after creation.  
If correction is needed, create new evidence with explanation.

### Invariant 4: ADR Immutability

ADR files are never rewritten.  
Changes are made via new ADR or status update (PROPOSED → ACCEPTED → SUPERSEDED).

### Invariant 5: Current Context Reflects Only Current State

CURRENT_CONTEXT reflects only the current operational state.  
It does not contain historical information or procedures.

### Invariant 6: Project Protocol Independence

PROJECT_PROTOCOL does not depend on current project state.  
It defines identity, not status.

### Invariant 7: Engineering Procedures in Engineering Documents

All engineering procedures live only in Engineering Knowledge documents (Layer 3).  
They do not appear in Project Identity or Operational Knowledge.

### Invariant 8: Procedures Are Not Source of Truth

Procedures are never the source of truth.  
The source of truth is only Core documents (Layers 1-2) and Evidence (Layer 4).

### Invariant 9: Authority and Maintainer Separation

Every document has an Authority (who defines content) and a Maintainer (who updates it).  
These are roles, not people. One participant may hold multiple roles.

### Invariant 10: Single Document Change

Changing a document must not require changing multiple independent documents.  
If it does, the architecture has a duplication problem.

### Invariant 11: One Primary Question

Every document must answer one primary question.  
This prevents scope creep and ensures focus.

### Invariant 12: Authority Flows Downward

Authority flows downward.  
Information may flow upward only as evidence.

Lower layers cannot redefine higher-layer concepts.  
They can only provide evidence that may inform higher-layer decisions.

Example:
- ENGINEERING_PLAYBOOK (Layer 3) cannot change PROJECT_PROTOCOL (Layer 1)
- ENGINEERING_PLAYBOOK can only reference PROJECT_PROTOCOL
- If a change is needed, it must be made at Layer 1 by the Authority


## Authority & Maintainer

Every document has two distinct roles:

**Authority:** The role that defines the content and structure of the document.  
**Maintainer:** The role that performs updates and corrections.

**Important:** Authority and Maintainer denote project roles, not specific individuals. One participant may hold multiple roles, and a role may be transferred to another participant without changing the documentation architecture.

### Role Assignments

| Document | Authority | Maintainer |
|---|---|---|
| PROJECT_PROTOCOL.md | Project Architect | Project Maintainer |
| CURRENT_CONTEXT.md | Project Architect | Project Maintainer |
| CODE_INDEX.md | Repository Maintainer | Repository Maintainer |
| RELEASES.md | Release Manager | Release Manager |
| ADR_INDEX.md | Project Architect | Project Maintainer |
| DOCUMENTS.md | Documentation Lead | Documentation Maintainer |
| REPOSITORIES.md | Infrastructure Lead | Infrastructure Maintainer |
| ENGINEERING_PLAYBOOK.md | Engineering Lead | Engineering Maintainer |
| DOC_STANDARD.md | Documentation Lead | Documentation Maintainer |
| RELEASE_PROCESS.md | Release Manager | Release Maintainer |
| AUTOMATION.md | Engineering Lead | Engineering Maintainer |
| ENGINEERING_HISTORY.md | Engineering Lead | Engineering Maintainer |
| evidence/ | QA / Verification | Verification System |

---

## Evolution

Documents may evolve through their lifecycle. The following operations are permitted:

### Permitted Operations

**Create:** A new document is added to the system.  
**Update:** An existing document is modified within its scope.  
**Archive:** A document is marked as ARCHIVED but preserved for historical reference.  
**Replace:** A document is superseded by a new document with a different name.  
**Split:** A document is divided into multiple documents when it grows beyond its scope.  
**Merge:** Multiple documents are combined when their scopes overlap.

### Prohibited Operations

**Rename:** A document is never renamed.  
Renaming breaks references and violates the single canonical source principle.

If a document needs a new name:
1. Archive the old document
2. Create a new document with the new name
3. Update all references

### Version Control

Documents are tracked via git.  
Major structural changes require a new version (e.g., INFORMATION_ARCHITECTURE_V2.md).  
Minor updates are tracked via git history.


## Compactness Principle

Every document must remain readable and have a single coherent theme.

**Rule:** If multiple independent themes appear within a document, they must be extracted into separate documents.

This principle ensures that documents do not grow uncontrollably and remain focused on their primary question.

---

## Creation Order

Documents are created in a specific order to ensure that each document has a ready contract from the Information Architecture before it is created:

    INFORMATION_ARCHITECTURE (Layer 0: Meta Architecture)
        ↓
    PROJECT_PROTOCOL (Layer 1: Project Identity)
        ↓
    DOCUMENTS (Layer 2: Operational Knowledge)
        ↓
    REPOSITORIES (Layer 2: Operational Knowledge)
        ↓
    ENGINEERING_PLAYBOOK (Layer 3: Engineering Knowledge)
        ↓
    DOC_STANDARD (Layer 3: Engineering Knowledge)
        ↓
    RELEASE_PROCESS (Layer 3: Engineering Knowledge)
        ↓
    AUTOMATION (Layer 3: Engineering Knowledge)

Each subsequent document is created with a pre-defined contract from this Information Architecture.

---

## Future Evolution

The information architecture is expected to evolve by:

- Introducing new document types
- Introducing new registries (e.g., SKILL_REGISTRY, MODEL_REGISTRY)
- Introducing generated documentation
- Introducing agent-maintained documentation
- Automating registry updates from code analysis

All evolution must preserve the 12 Information Invariants.

The architecture is designed to accommodate growth without fundamental restructuring. New documents must fit into the existing layer model and lifecycle categories.

---

## End of Document

This document defines the information architecture of the Agent Developer project.  
It is the foundation upon which all other documentation is built.  
All other documents must conform to the principles and invariants defined herein.

