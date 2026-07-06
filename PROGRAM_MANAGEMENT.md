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

**Engineering Invariant:** Every engineering program follows a defined lifecycle and is governed exclusively by the rules in this document.

---

## End of Document
