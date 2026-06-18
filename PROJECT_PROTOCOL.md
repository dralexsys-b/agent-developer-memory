# Project Protocol

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Project Architect  
**Maintainer:** Project Maintainer  

**Type:** Protocol (Layer 1: Project Identity)  
**Primary Question:** "What is this project?"  
**Canonical Source for:** Engineering Principles, Roles, Source of Truth hierarchy  
**Dependencies:** INFORMATION_ARCHITECTURE.md (Layer 0)  
**Dependents:** All other documents  

---

## Project Overview

### Mission

Agent-Developer exists to create a local, self-hosted AI system capable of autonomous software development through a deterministic, verifiable, and reproducible engineering process.

The project aims to prove that complex software systems can be built by AI agents working within strict engineering constraints, with full transparency and evidence-based decision making.

### Vision

The long-term vision is a multi-agent system where:

- Specialized agents (Developer, Tester, Architect, Reviewer) collaborate through well-defined protocols
- Every architectural decision is documented as ADR
- Every change is verified through evidence
- The system can reproduce any previous state from evidence logs
- Engineering knowledge accumulates and improves over time

### Scope

**In scope:**
- Local AI agent development on AMD hardware (ROCm + llama.cpp)
- Deterministic orchestration pipelines (LangGraph)
- Evidence-based engineering process
- Architecture documentation and ADR system
- Reproducible build and verification workflows

**Out of scope:**
- Dependence on proprietary cloud services as a required runtime component
- Non-deterministic multi-agent swarms
- Production deployment of AI-generated code without human approval
- Real-time collaborative editing between multiple human developers


---

## Примечание

Данный документ является первой консолидированной версией протокола проекта.

На этапе становления архитектуры допускается временное объединение нескольких тематических разделов в одном документе для упрощения проектирования и согласования.

По мере развития проекта документ будет рефакториться без изменения его контрактов. Независимые темы будут переноситься в специализированные документы в соответствии с принципами, определёнными в INFORMATION_ARCHITECTURE.md.

До завершения формирования системы документации допускаются временные отклонения от принципа компактности документов, если это упрощает проектирование архитектуры и не нарушает установленные контракты документов.


## Roles & Decision Authority

### Role Hierarchy

The project operates with three distinct roles, each with specific responsibilities and decision authority:

#### Architect (ChatGPT)

**Responsibilities:**
- Defines project architecture and information structure
- Approves architectural decisions (ADR)
- Reviews and approves protocols and standards
- Declares stable baselines and releases
- Resolves architectural conflicts

**Decision Authority:**
- Architecture changes
- Protocol modifications
- ADR approval
- Baseline declaration
- Release approval

#### Engineer (Qwen)

**Responsibilities:**
- Implements approved architecture according to protocols
- Follows Engineering Playbook procedures
- Generates evidence for all changes
- Maintains documentation according to DOC_STANDARD
- Requests clarification when architecture is ambiguous

**Decision Authority:**
- Implementation details within approved architecture
- Bug fixes (local patches)
- Documentation updates (within scope)
- Evidence generation

**Constraint:**
Qwen does NOT make architectural decisions independently. When encountering ambiguity, Qwen must request clarification from the Architect rather than introducing architectural changes.

#### Executor (User)

**Responsibilities:**
- Executes approved commands on the server
- Validates evidence and test results
- Provides final approval for irreversible operations
- Manages infrastructure (hardware, network, storage)

**Decision Authority:**
- Command execution on server
- Infrastructure management
- Evidence validation

---

### Decision Authority Matrix

| Decision Type | Architect | Engineer | Executor |
|---|---|---|---|
| Architecture changes | ✅ Approves | 📝 Proposes | ⚙️ Executes commands |
| Protocol modifications | ✅ Approves | 📝 Proposes | ⚙️ Executes commands |
| ADR creation | ✅ Approves | 📝 Drafts | 📋 Acknowledges |
| Baseline declaration | ✅ Declares | 📝 Suggests | 📋 Acknowledges |
| Release approval | ✅ Approves | 📝 Prepares | ⚙️ Executes commands |
| Implementation details | 🔍 Reviews | ✅ Decides | ⚙️ Executes commands |
| Bug fixes (local patches) | 🔍 Reviews | ✅ Decides | ⚙️ Executes commands |
| Documentation updates | 🔍 Reviews | ✅ Decides | 📋 Acknowledges |
| Evidence generation | 🔍 Reviews | ✅ Generates | ✅ Validates |
| Command execution | N/A | N/A | ⚙️ Executes commands |
| Infrastructure management | N/A | N/A | ✅ Decides |


## Engineering Principles

The following 12 principles guide all engineering decisions in the project. These are not rules, but philosophy — the foundation upon which all procedures are built.

### 1. Evidence First

Every claim must be backed by verifiable evidence.  
No assumption is accepted without proof.  
No "it should work" — only "here is the log showing it works."

### 2. ADR before Implementation

Architectural decisions are made before code is written.  
Every significant design choice is documented as an ADR (Architecture Decision Record).  
Implementation follows approved architecture, not the other way around.

### 3. One Logical Change

One revision contains one logical change.  
No batch changes. No "while I'm here, let me also fix..."  
If multiple changes are needed, they are split into separate revisions.

### 4. Local Patch before Rewrite

A local patch is always preferred over rewriting the entire file.  
Full rebuilds are only permitted when architectural changes require them.  
The principle: minimize change surface area.

### 5. Facts over Assumptions

Facts from evidence are more important than assumptions made by any model or human.  
When evidence contradicts expectation, trust the evidence.

### 6. Automation after Repetition

If a command sequence has been executed three times, it must be automated.  
Manual repetition is a sign that automation is needed.  
Evolution: manual command → copy-paste → script → utility.

### 7. Architecture before Optimization

First build a stable, correct architecture.  
Then optimize.  
Optimization without stable architecture leads to technical debt.

### 8. Maintainability is a Feature

Code and documentation must be maintainable.  
Complexity without justification is a bug.  
Readability is more important than cleverness.

### 9. Reproducibility over Convenience

Every result must be reproducible.  
If you cannot reproduce it, you do not understand it.  
Convenience shortcuts that break reproducibility are forbidden.

### 10. Small Verified Steps

Large changes are forbidden.  
Large changes are made as a sequence of small, verified steps.  
Each step is verified before proceeding to the next.

### 11. Every Fact Has Exactly One Canonical Source

Every piece of information lives in exactly one document.  
Other documents may reference it, but never duplicate it.  
Duplication is an architectural error.

### 12. Authority Flows Downward, Evidence Flows Upward

Higher layers define rules for lower layers.  
Lower layers cannot redefine higher-layer concepts.  
Lower layers can only provide evidence that may inform higher-layer decisions.

Example: ENGINEERING_PLAYBOOK (Layer 3) cannot change PROJECT_PROTOCOL (Layer 1).  
It can only reference PROJECT_PROTOCOL and provide evidence that may lead to changes at Layer 1.


## Source of Truth

When multiple sources of information exist, conflicts may arise. This section defines which sources own which facts and how to resolve contradictions.

### Canonical Sources

Every fact in the project has exactly one Canonical Source — the unique document that owns it. Other documents may reference the fact, but never duplicate it.

| Fact Domain | Canonical Source | Layer |
|---|---|---|
| Project identity, roles, principles | PROJECT_PROTOCOL.md | Layer 1 |
| Current operational state | CURRENT_CONTEXT.md | Layer 2 |
| File registry | CODE_INDEX.md | Layer 2 |
| Release history | RELEASES.md | Layer 2 |
| Architecture decisions | ADR_INDEX.md | Layer 2 |
| Repository registry | REPOSITORIES.md | Layer 2 |
| Documentation registry | DOCUMENTS.md | Layer 2 |
| Engineering procedures | ENGINEERING_PLAYBOOK.md | Layer 3 |
| Documentation standards | DOC_STANDARD.md | Layer 3 |
| Release procedures | RELEASE_PROCESS.md | Layer 3 |
| Automation rules | AUTOMATION.md | Layer 3 |
| Engineering knowledge | ENGINEERING_HISTORY.md | Layer 3 |
| Verification evidence | evidence/ | Layer 4 |

### Conflict Resolution

When two sources of information contradict each other, follow this algorithm:

**Step 1: Identify the conflicting fact.**  
Determine which specific piece of information is in dispute.

**Step 2: Find the Canonical Source.**  
Consult the table above. The document listed as Canonical Source for that fact domain is the authoritative owner.

**Step 3: Trust the Canonical Source.**  
If the Canonical Source exists and is current, its version of the fact is the truth. All other documents must be updated to conform.

**Step 4: Apply priority hierarchy if Canonical Source is absent or outdated.**  
If the fact has no clear Canonical Source, or the Canonical Source is clearly outdated, use the following priority (highest to lowest):

1. **Runtime Behavior** — the actual behavior of the system
2. **Evidence** — logs, test results, benchmarks (Layer 4)
3. **ADR** — approved architectural decisions
4. **Documentation** — protocols, playbooks, standards
5. **Conversation** — chat messages, verbal agreements

**Step 5: Escalate if unresolved.**  
If the conflict cannot be resolved by the above steps, escalate to the Architect (ChatGPT) for a decision. The Architect may:
- Clarify the Canonical Source
- Create a new ADR to resolve the ambiguity
- Update the information architecture

**Principle:** Procedures (Layer 3) are never the source of truth. They describe how to act, but the truth comes from Core documents (Layers 1-2) and Evidence (Layer 4).


## Documentation Map

The project follows the information architecture defined in `INFORMATION_ARCHITECTURE.md` (Layer 0).

For a complete registry of all project documents, see `DOCUMENTS.md` (planned document, Layer 2).

### Document Types

Every document belongs to one of the following types:

- **Protocol** — defines rules of interaction and responsibilities
- **Standard** — defines requirements for artifacts
- **Playbook** — defines sequence of actions
- **Architecture** — defines system structure
- **Index** — helps find information (navigation)
- **Registry** — authoritative inventory of project entities
- **History** — records past events
- **Context** — describes current state

When creating a new document, first determine its type, then assign a name.

---

## Repositories

For the authoritative registry of project repositories, see `REPOSITORIES.md` (planned document, Layer 2).

### Current Repositories

- **agent-developer-memory** — documentation, ADR, evidence, protocols
- **agent-developer-runtime** — source code, orchestrators, tools

Each repository has a specific purpose and is managed according to the principles defined in this protocol.


## Document Lifecycle

This document (PROJECT_PROTOCOL.md) is classified as **Static** according to the Knowledge Lifecycle defined in INFORMATION_ARCHITECTURE.md.

### Permitted Changes

This document may be:
- **Clarified** — improving wording without changing meaning
- **Extended** — adding new sections when new architectural concerns arise
- **Deprecated** — marked as superseded by a newer version
- **Amended via appendix** — additional clarifications added at the end

This document may NOT be:
- **Completely rewritten** — if fundamental changes are needed, create PROJECT_PROTOCOL_V2.md

### Version Control

Changes to this document require approval from the Architect role.  
All changes are tracked via git history.  
Major structural changes require a new version number.

---

## Relationship to Other Documents

This document (PROJECT_PROTOCOL.md) serves as the foundation for all other project documentation:

- **INFORMATION_ARCHITECTURE.md** (Layer 0) — defines the structure in which this document lives
- **CURRENT_CONTEXT.md** (Layer 2) — reflects current operational state in accordance with this protocol
- **ENGINEERING_PLAYBOOK.md** (Layer 3) — defines engineering procedures following principles from this protocol
- **All other documents** — must conform to the roles, principles, and source of truth hierarchy defined here

This document does NOT contain:
- Current project status (see CURRENT_CONTEXT.md)
- Engineering procedures (see ENGINEERING_PLAYBOOK.md)
- Release procedures (see RELEASE_PROCESS.md)
- Documentation standards (see DOC_STANDARD.md)
- Specific architectural decisions (see ADR_INDEX.md)

---

## End of Document

This document defines the project identity, roles, engineering principles, and source of truth hierarchy for the Agent Developer project.

It is the authoritative reference for:
- Who makes which decisions
- What principles guide engineering work
- How to resolve conflicts between information sources
- What this project is and what it is not

All other documents must conform to the framework established herein.

