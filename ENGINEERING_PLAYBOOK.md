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

1. **Follow PROJECT_PROTOCOL principles** — all 12 principles apply
2. **Write tests first** — TDD Red Phase: failing tests define expected behavior
3. **Make small changes** — one logical change per commit (Principle #3)
4. **Prefer local patches** — minimize change surface area (Principle #4)
5. **Implement minimal solution** — TDD Green Phase: simplest code that passes tests
6. **Refactor** — TDD Refactor Phase: improve code while keeping tests green
7. **Generate evidence** — logs, test results, benchmarks (Principle #1)

### Phase 3: Verification

1. **Run verification pipeline** — execute the project's mandatory verification process
2. **Verify all checks pass** — implementation must satisfy verification requirements
3. **Update affected documentation**
4. **Create commit** — record the verified implementation
5. **Push to repository** — after successful verification

### Phase 4: Review

1. **Request review** — from Architect or peer (detailed procedures are defined in the applicable project standards)
2. **Address feedback** — make corrections if needed
3. **Merge to main** — after approval
4. **Update CURRENT_CONTEXT.md** — if operational state changed


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

### Verification Pipeline

The verification pipeline is a mandatory process executed before every commit:

1. **Execute pipeline** — run all verification stages defined for the project
2. **Verify success** — all stages must pass; partial success is not acceptable
3. **Treat as mandatory** — verification cannot be skipped or bypassed

The composition of the verification pipeline is defined by the project and may evolve over time. This playbook defines the requirement to perform verification, while project-specific engineering documents define the concrete verification stages.

**Engineering Invariant:** Verification is mandatory. No exceptions.

### Verification Stages

Verification is composed of one or more stages defined by the project.

Typical stages include:

1. Code quality verification
2. Static analysis
3. Automated testing
4. Public contract validation

The exact set of stages is project-specific and may evolve over time.

**Engineering Invariant:** Every verification stage defined by the project must complete successfully before changes are accepted.

### Smoke Testing

Smoke tests validate the public contract of the system:

1. **Test public interface** — validate external behavior, not internal implementation
2. **Protect public contract** — breaking changes require explicit approval
3. **Ensure isolation** — tests must not modify system state
4. **Use realistic scenarios** — test with actual project artifacts

Smoke testing verifies that externally observable behavior remains consistent after change. The concrete implementation of smoke tests is project-specific.

**Engineering Invariant:** Public contract is protected by smoke tests.

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

### Shell Scripting Standards

Shell scripts should follow consistent engineering practices to ensure reliability, readability, and maintainability.

1. **Use an appropriate interpreter** — declare the required shell explicitly.
2. **Fail predictably** — scripts should stop on unrecoverable errors.
3. **Quote variable expansions** — avoid unintended word splitting and glob expansion.
4. **Handle errors explicitly** — provide meaningful diagnostics for failures.
5. **Design for idempotence** — repeated execution should produce a predictable result.
6. **Manage temporary resources safely** — create and clean up temporary files reliably.
7. **Document script purpose** — describe usage, dependencies, inputs and outputs.

Project-specific implementation details (strict mode, shellcheck configuration, verify.sh, etc.) are documented in AUTOMATION.md.

**Engineering Invariant:** Shell scripting practices must be applied consistently across the project.

#### Heredoc Usage

Before creating a heredoc, determine the type of artifact being produced:

1. **Code heredoc** — formatting follows the target programming language (e.g., indentation belongs to the generated code, not to the heredoc mechanism).
2. **Text heredoc** — formatting follows the target document format (commit messages, Markdown, YAML, plain text).
3. **The heredoc mechanism must never influence the formatting of the generated artifact.**

Formatting rules apply to the generated artifact, not to the heredoc syntax itself.

### Git Workflow

Git history is part of the engineering documentation and must remain understandable over time.

1. **One engineering concept per commit** — each commit introduces one coherent engineering idea
2. **Keep commits atomic** — changes should be reviewable and reversible
3. **Write meaningful commit messages** — explain why the change exists, not only what changed
4. **Review before publishing** — verify the working tree and review the diff before commit
5. **Keep history clean** — avoid unrelated changes within the same commit

Project-specific branching strategies and release procedures are documented in PROJECT_PROTOCOL.md and RELEASE_PROCESS.md.

**Engineering Invariant:** Git history must clearly communicate the evolution of the project.

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

## References

For detailed engineering procedures, see the following Layer 3 documents:

- **DOC_STANDARD.md** — documentation standards, formatting requirements, review checklists
- **RELEASE_PROCESS.md** — release procedures, versioning, deployment steps
- **AUTOMATION.md** — automated scripts, CI/CD pipelines, triggers
- **ENGINEERING_HISTORY.md** — lessons learned, post-mortems, retrospectives

These documents are defined in INFORMATION_ARCHITECTURE.md and will be created according to the project roadmap.

## End of Document

This document defines the engineering procedures for the Agent Developer project.

It is the authoritative reference for:
- How to develop the project (general workflow)
- How to manage changes (types and procedures)
- How to test and verify (general principles)
- Best practices and common pitfalls

For detailed procedures, see the Layer 3 documents listed in the References section.

All engineering work must conform to the procedures defined herein.

