# Engineering Playbook

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Engineering Lead  
**Maintainer:** Engineering Maintainer  

**Type:** Playbook (Layer 3: Engineering Knowledge)  
**Primary Question:** "How do we develop this project?"  
**Canonical Source for:** Development workflow, change procedures, best practices  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md  
**Dependents:** DOC_STANDARD.md, RELEASE_PROCESS.md, AUTOMATION.md  

---

## Development Workflow

The development workflow follows a structured process from idea to deployment:

### Phase 0: Documentation First

1. **Create specification** — document requirements before implementation
2. **Define acceptance criteria** — what does "done" look like?
3. **Identify dependencies** — what documents need updates?
4. **Get approval** — Architect reviews specification before implementation begins

### Phase 1: Planning

1. **Identify the need** — what problem are we solving?
2. **Check existing documentation** — does this conflict with PROJECT_PROTOCOL?
3. **Create ADR if needed** — architectural decisions require ADR (see PROJECT_PROTOCOL Principle #2)
4. **Define scope** — what changes are needed? (see Principle #3: One Logical Change)

### Phase 2: Implementation

5. **Follow PROJECT_PROTOCOL principles** — all 12 principles apply
6. **Make small changes** — one logical change per commit (Principle #3)
7. **Prefer local patches** — minimize change surface area (Principle #4)
8. **Generate evidence** — logs, test results, benchmarks (Principle #1)

### Phase 3: Verification

9. **Test the changes** — verify correctness (Principle #9: Reproducibility)
10. **Update documentation** — if needed (see Documentation Updates section)
11. **Create commit** — clear message, atomic change
12. **Push to repository** — with evidence attached

### Phase 4: Review

13. **Request review** — from Architect or peer (detailed procedures are defined in the applicable project standards)
14. **Address feedback** — make corrections if needed
15. **Merge to main** — after approval
16. **Update CURRENT_CONTEXT.md** — if operational state changed


---

## Change Management

All changes to the project must follow these procedures:

### Types of Changes

**Architectural Changes:**
- Require ADR (Architecture Decision Record)
- Must be approved by Architect role
- May require updates to PROJECT_PROTOCOL or INFORMATION_ARCHITECTURE
- Examples: new document types, layer restructuring, role changes

**Implementation Changes:**
- Follow approved architecture
- Must be approved by Engineer role
- Require evidence (logs, test results)
- Examples: bug fixes, feature additions, refactoring

**Documentation Changes:**
- Must conform to applicable project standards (when defined)
- Require approval from document Authority
- Examples: clarifications, corrections, extensions

### Change Procedure

1. **Identify change type** — architectural, implementation, or documentation
2. **Check dependencies** — does this affect other documents?
3. **Follow PROJECT_PROTOCOL principles** — all 12 principles apply
4. **Make the change** — small, verified steps
5. **Generate evidence** — logs, test results, benchmarks
6. **Update affected documents** — if Canonical Source changed
7. **Commit with clear message** — explain what and why
8. **Push to repository** — with evidence attached


---

## Testing & Verification

All changes must be verified before merging:

### General Principles

1. **Every change needs evidence** — logs, test results, benchmarks (Principle #1)
2. **Reproducibility is mandatory** — if you can't reproduce it, you don't understand it (Principle #9)
3. **Small verified steps** — verify each step before proceeding (Principle #10)
4. **Facts over assumptions** — trust evidence, not expectations (Principle #5)

### Testing Levels

**Unit Testing:**
- Test individual functions and modules
- Verify correctness of implementation
- Generate evidence (test logs)

**Integration Testing:**
- Test interaction between components
- Verify end-to-end functionality
- Generate evidence (integration logs)

**Performance Testing:**
- Test speed, memory usage, throughput
- Verify performance requirements
- Generate evidence (benchmark logs)

### Evidence Requirements

**For Implementation Changes:**
- Test logs (unit, integration, performance)
- Benchmark results (if applicable)
- Reproduction steps

**For Documentation Changes:**
- Markdown validation (no syntax errors)
- Link validation (all references work)
- Consistency check (no contradictions)

**For Architectural Changes:**
- Impact assessment (which documents affected)
- Migration plan (how to update existing documents)
- Approval from Architect


---

## Best Practices

### General Principles

1. **Follow PROJECT_PROTOCOL** — all 12 principles apply
2. **Make small changes** — one logical change per commit
3. **Generate evidence** — every claim needs proof
4. **Update documentation** — keep it in sync with code
5. **Request review** — don't merge without approval

### Common Pitfalls

**Avoid:**
- Large batch changes (break into small steps)
- Duplicating facts (use Canonical Source)
- Skipping evidence (every change needs proof)
- Merging without review (always get approval)
- Ignoring documentation (keep it up-to-date)

**Prefer:**
- Local patches over rewrites
- Small verified steps over large changes
- Evidence over assumptions
- Clear commit messages over vague ones
- Consistent formatting over creative styles

### Tools & Automation

**Use:**
- Git for version control
- Markdown for documentation
- Logs for evidence
- Scripts for automation (when repetition occurs)

**Avoid:**
- Manual repetition (automate after 3 times)
- Unverified assumptions (generate evidence)
- Complex workflows (keep it simple)


---

## References

For detailed engineering procedures, see the following Layer 3 documents:

- **DOC_STANDARD.md** — documentation standards, formatting requirements, review checklists
- **RELEASE_PROCESS.md** — release procedures, versioning, deployment steps
- **AUTOMATION.md** — automated scripts, CI/CD pipelines, triggers
- **ENGINEERING_HISTORY.md** — lessons learned, post-mortems, retrospectives

These documents are defined in INFORMATION_ARCHITECTURE.md and will be created according to the project roadmap.

---

## End of Document

This document defines the engineering procedures for the Agent Developer project.

It is the authoritative reference for:
- How to develop the project (general workflow)
- How to manage changes (types and procedures)
- How to test and verify (general principles)
- Best practices and common pitfalls

For detailed procedures, see the Layer 3 documents listed in the References section.

All engineering work must conform to the procedures defined herein.

