# Program Management

**Status:** DRAFT
**Version:** 1.0
**Date:** 2026-07-06
**Authority:** Project Architect
**Maintainer:** Project Maintainer

**Type:** Standard (Layer 3: Engineering Knowledge)
**Primary Question:** "How do we manage engineering programs?"
**Canonical Source for:** Program management rules, lifecycle, governance
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, ENGINEERING_PLAYBOOK.md
**Dependents:** PROGRAMS.md

---

## Purpose

This document defines the rules and processes for managing engineering programs in the Agent Developer project.

This document is the canonical source for engineering program governance within the Agent Developer project.

It answers the question: **How do we manage engineering programs?**

This document does NOT define:
- Specific programs (see PROGRAMS.md)
- Individual program plans (each program has its own document)
- Runtime architecture or implementation details
- Engineering processes (see ENGINEERING_PLAYBOOK.md)
- Project governance (defined by PROJECT_GOVERNANCE)

---

## Scope

This document defines:
- What constitutes a program
- Program lifecycle states
- State transition rules
- Governance rules for frozen programs
- Backlog management
- Review and retrospective requirements

This document does NOT define:
- Specific program content
- Implementation details
- Technical architecture
- Day-to-day engineering practices
- Project governance

---

## Place in Architecture

This document sits at the intersection of project governance and engineering execution:

PROJECT_GOVERNANCE
        ↓
INFORMATION_ARCHITECTURE
        ↓
PROGRAM_MANAGEMENT  ← this document
       ↙        ↘
PROGRAMS.md   Individual Program Plans

**Relationship to other documents:**

- **PROJECT_GOVERNANCE** defines overall project authority and decision-making
- **INFORMATION_ARCHITECTURE** defines how documentation is organized
- **ENGINEERING_PLAYBOOK** defines how engineering work is performed
- **PROGRAM_MANAGEMENT** defines how programs are managed through their lifecycle
- **PROGRAMS.md** is the registry of all programs (governed by this document)
- **Individual Program Plans** are governed by the rules defined here

**Engineering Invariant:** Every engineering program follows the lifecycle defined in this document.

---

## Terminology

### Program

**Definition:**
A Program is the highest-level planning unit used to organize a bounded engineering effort toward a single architectural goal.

**Role:**
Programs are the primary organizational unit used to plan, execute and evaluate engineering work. Every program operates under the governance rules defined in this document.

---

### Program Plan

**Definition:**
A Program Plan is the authoritative execution plan that defines how a program will be delivered, including its phases, milestones, commits, and exit criteria.

**Role:**
The Program Plan serves as the authoritative engineering plan that defines how a program will be executed.

---

### Phase

**Definition:**
A Phase divides a program into sequential engineering stages, each with a clear objective that must be completed before the next phase begins unless explicitly defined otherwise.

**Role:**
Phases provide structure within a program, allowing work to be organized into coherent units with distinct objectives and deliverables.

---

### Milestone

**Definition:**
A Milestone represents a formal engineering decision point or completion point that changes the state or progress of a program.

**Role:**
Milestones provide visibility into program progress and trigger state transitions. They represent binary achievements that mark significant points in the program lifecycle.

---

### Backlog

**Definition:**
A Backlog is a collection of potential future programs and ideas that have not yet been committed to execution.

**Role:**
The Backlog serves as the input source for future programs, capturing ideas that may become programs in subsequent planning cycles. It is distinct from active programs.

---

### Review

**Definition:**
A Review is a formal evaluation conducted at specific points in a program's lifecycle to assess progress, quality, and alignment with goals.

**Role:**
Reviews provide governance checkpoints where decisions are made about program execution, scope adjustments, and risk management.

---

### Retrospective

**Definition:**
A Retrospective is a structured reflection conducted after program completion to capture lessons learned and improve future programs.

**Role:**
Retrospectives answer the question "What did we learn?" by systematically analyzing what went well, what could be improved, and what recommendations should inform future programs.

---

## End of Document
