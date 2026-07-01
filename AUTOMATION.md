# Automation

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Engineering Lead  
**Maintainer:** Engineering Maintainer  

**Type:** Playbook (Layer 3: Engineering Knowledge)  
**Primary Question:** "What is automated and how is automation organized?"  
**Canonical Source for:** Automated scripts, CI/CD pipelines, automation structure, triggers  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, ENGINEERING_PLAYBOOK.md, RELEASE_PROCESS.md  
**Dependents:** ENGINEERING_HISTORY.md  

---

## Automation Principles

The following principles guide automation decisions (see ENGINEERING_PLAYBOOK Principle #6):

### When to Automate

1. **After three repetitions** — if a command sequence has been executed manually three times, it must be automated
2. **Error-prone operations** — operations frequently causing mistakes
3. **Time-consuming tasks** — operations taking more than 5 minutes manually
4. **Critical paths** — operations on release, deployment, or verification paths

### What Not to Automate

1. **One-time operations** — setup of new infrastructure, migrations
2. **Exploratory tasks** — debugging, investigation
3. **Decision-dependent operations** — requiring human judgment
4. **Architectural decisions** — ADR creation, protocol changes

### Verification Automation

Verification automation defines how project verification is executed as a repeatable engineering process.

1. **Provide a unified verification process** — verification is executed through a consistent automation workflow.
2. **Coordinate verification stages** — automation runs the verification stages defined by the project.
3. **Produce engineering evidence** — verification generates evidence for engineering decisions.
4. **Fail predictably** — verification stops when a required stage fails.
5. **Remain deterministic** — repeated execution produces consistent results.

The concrete automation scripts, verification stages and execution order are documented in the corresponding sections of this document.

**Engineering Invariant:** Verification automation must produce reproducible engineering evidence.

---

## Automation Registry

The following automations exist in the project:

### Build Automations

| Automation | Purpose | Trigger | Repository |
|------------|---------|---------|------------|
| ROCm build automation | Build ROCm environment | Manual | Runtime |
| llama.cpp build automation | Build llama.cpp with ROCm support | Manual | Runtime |

### Runtime Automations

| Automation | Purpose | Trigger | Repository |
|------------|---------|---------|------------|
| Runtime startup automation | Start inference services | Manual | Runtime |
| Environment restoration | Restore runtime environment | Manual | Runtime |

### Benchmark Automations

| Automation | Purpose | Trigger | Repository |
|------------|---------|---------|------------|
| VRAM benchmark automation | Regression testing | Manual | Runtime |

### Evidence Automations

| Automation | Purpose | Trigger | Repository |
|------------|---------|---------|------------|
| Evidence collection | Collect runtime logs | Post-test | Runtime |

### Implementation Note

Each automation may consist of one or more scripts whose names may change over time.
This registry describes the automation functionality, not specific file names.
For current implementation details, see the runtime repository and its current project structure.

### Planned Automations

The following automations are planned but not yet implemented:

| Automation | Purpose | Status |
|------------|---------|--------|
| Documentation validation | Validate documentation structure | PLANNED |
| Cross-reference validation | Validate document links | PLANNED |
| CI/CD pipeline | Automated testing and deployment | PLANNED |

### Note

Registry reflects actual state of the project.
When new automation is added, it must be registered here.
When automation is removed or changed, registry must be updated.


---

## Automation Structure

All automation scripts follow this structure:

### Directory Layout

    agent-developer-runtime/
    ├── scripts/
    │   ├── build_*.sh              — build automations
    │   ├── start_*.sh              — runtime startup
    │   ├── restore_*.sh            — environment restoration
    │   ├── *_benchmark.sh          — benchmarking
    │   └── collect_*.sh            — evidence collection
    └── automation/                 — (future) advanced automations

### Naming Conventions

- Use `snake_case.sh` for shell scripts
- Use `snake_case.py` for Python scripts
- Use descriptive names that reflect purpose
- Prefix with category if needed: `build_`, `start_`, `restore_`, `vram_`, `collect_`

### Script Requirements

Every automation script must:

1. **Be idempotent** — running multiple times has same effect as running once
2. **Generate evidence** — produce logs for audit trail
3. **Fail fast** — exit on first error with clear message
4. **Be documented** — header comment explaining purpose, usage, dependencies
5. **Be testable** — can be run independently
6. **Follow DOC_STANDARD** — documentation in header


---

## Adding New Automation

When adding new automation, follow this procedure:

### Procedure

1. **Verify principle applies** — confirm automation is needed (3+ repetitions, error-prone, time-consuming, critical path)
2. **Check registry** — ensure similar automation doesn't exist
3. **Choose location** — `scripts/` for simple scripts, `automation/` for complex ones
4. **Follow naming conventions** — use `snake_case` with descriptive name
5. **Implement script** — satisfy all script requirements
6. **Generate evidence** — script must produce logs
7. **Test script** — verify idempotence, error handling, output
8. **Register in Automation Registry** — add entry to table in this document
9. **Update CURRENT_CONTEXT.md** — if operational state changed
10. **Commit with evidence** — include test logs

### Documentation Template

Every automation script must include this header:

    #!/bin/bash
    # Purpose: [one-line description]
    # Trigger: [manual/cron/CI/hook]
    # Dependencies: [required tools/libraries]
    # Evidence: [what logs are generated]
    # Author: [role]
    # Date: [creation date]


---

## Trigger Model

Automations can be triggered by different mechanisms:

### Existing Triggers

**Manual execution:**
- User runs script directly
- Used for: build, test, evidence collection
- Requires: user knowledge of script location and usage

### Planned Triggers

The following trigger mechanisms are planned but not yet implemented:

**Git Hook triggers:**
- Pre-commit: documentation validation
- Post-commit: link validation
- Pre-push: test suite

**CI/CD triggers:**
- On push to main: full test suite, build
- On PR: subset of tests
- On tag: release pipeline

**Scheduled triggers:**
- Cron jobs for routine maintenance
- Periodic evidence collection
- Scheduled backups

---

## End of Document

This document defines the automation for the Agent Developer project.

It is the authoritative reference for:
- Automation principles (when to automate, what not to automate)
- Automation registry (existing and planned automations)
- Automation structure (directory layout, naming, requirements)
- Procedure for adding new automation
- Trigger model (existing: manual; planned: git hooks, CI/CD, scheduled)

All automation must conform to the rules defined herein.

