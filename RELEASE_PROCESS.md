# Release Process

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Engineering Lead  
**Maintainer:** Engineering Maintainer  

**Type:** Playbook (Layer 3: Engineering Knowledge)  
**Primary Question:** "How do we release?"  
**Canonical Source for:** Release procedures, versioning, deployment steps, verification  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, ENGINEERING_PLAYBOOK.md, DOC_STANDARD.md  
**Dependents:** AUTOMATION.md, ENGINEERING_HISTORY.md  

---

## Release Types

The project uses the following release types:

### Major Release (X.0.0)

- Significant architectural changes
- Breaking changes to APIs or interfaces
- New major features that change system behavior
- Requires full regression testing
- Examples: 1.0.0, 2.0.0, 3.0.0

### Minor Release (X.Y.0)

- New features without breaking changes
- Significant improvements to existing functionality
- Requires integration testing
- Examples: 1.1.0, 1.2.0, 2.1.0

### Patch Release (X.Y.Z)

- Bug fixes
- Security patches
- Performance improvements
- Documentation updates
- Requires unit testing
- Examples: 1.0.1, 1.1.2, 2.0.3

### Hotfix Release (X.Y.Z-hotfix.N)

- Critical bug fixes requiring immediate deployment
- Bypass normal release cycle
- Requires minimal testing (focused on fix)
- Must be followed by proper patch release
- Examples: 1.0.1-hotfix.1, 2.1.3-hotfix.2


---

## Versioning Scheme

The project follows Semantic Versioning (SemVer) principles:

### Version Format

    MAJOR.MINOR.PATCH[-hotfix.N]

### Version Components

**MAJOR** — incremented when:
- Making incompatible API changes
- Introducing breaking changes
- Major architectural shifts

**MINOR** — incremented when:
- Adding functionality in a backward-compatible manner
- Significant feature additions
- No breaking changes

**PATCH** — incremented when:
- Making backward-compatible bug fixes
- Security patches
- Performance improvements
- Documentation updates

**hotfix.N** — optional suffix for:
- Emergency fixes deployed outside normal cycle
- N is sequential counter (1, 2, 3...)
- Must be replaced by proper PATCH release

### Tagging

- All releases must be tagged in git
- Tag format: `vX.Y.Z` or `vX.Y.Z-hotfix.N`
- Tags are immutable once created
- Tags must point to stable commits on main branch


---

## Release Workflow

The release process follows these phases:

### Phase 1: Preparation

1. **Identify release scope** — what changes are included?
2. **Verify all changes merged** — no pending PRs for this release
3. **Update documentation** — ensure all docs reflect current state
4. **Update release documentation** — list all changes since last release
5. **Bump version** — update version in relevant files

### Phase 2: Verification

6. **Run full test suite** — all tests must pass
7. **Generate evidence** — collect test logs, benchmarks
8. **Verify reproducibility** — build from clean state
9. **Review documentation** — ensure accuracy and completeness
10. **Get approval** — Architect role approves release

### Phase 3: Release

11. **Create release branch** (if needed) — for major/minor releases
12. **Create git tag** — follow versioning scheme
13. **Build release artifacts** — compile, package, prepare
14. **Verify artifacts** — test built artifacts
15. **Publish release** — deploy, distribute, announce

### Phase 4: Post-release

16. **Update CURRENT_CONTEXT.md** — reflect new baseline
17. **Update release documentation** — add release entry
18. **Monitor for issues** — watch for post-release problems
19. **Document lessons learned** — add to ENGINEERING_HISTORY.md
20. **Plan next iteration** — identify next release scope


---

## Pre-release Checklist

Before creating a release, verify the following:

### Code Quality

- [ ] All tests pass (unit, integration, performance)
- [ ] No known critical bugs
- [ ] Code review completed for all changes
- [ ] No TODO comments blocking release
- [ ] All evidence collected and stored

### Documentation

- [ ] Release documentation updated with all changes
- [ ] README reflects current state
- [ ] All documentation conforms to DOC_STANDARD
- [ ] Cross-references are valid
- [ ] Version numbers updated where needed

### Build & Deployment

- [ ] Build succeeds from clean state
- [ ] Release artifacts created successfully
- [ ] Artifacts verified (tested, validated)
- [ ] Deployment procedure tested
- [ ] Rollback procedure documented

### Approval

- [ ] Architect role approved release
- [ ] All stakeholders notified
- [ ] Release notes prepared
- [ ] Communication plan ready


---

## Post-release Actions

After a release is published:

1. **Update CURRENT_CONTEXT.md** — set new baseline
2. **Update release documentation** — add release entry with version, date, summary, and evidence link
3. **Monitor systems** — watch for issues in first 24 hours
4. **Collect feedback** — gather user reports, error logs
5. **Document lessons learned** — add to ENGINEERING_HISTORY.md
6. **Plan next iteration** — identify scope for next release

---

## Hotfix Procedure

For critical bugs requiring immediate fix:

### Hotfix Workflow

1. **Identify critical issue** — must be production-blocking
2. **Create hotfix branch** — from release tag
3. **Implement minimal fix** — only fix the issue, no other changes
4. **Test focused scope** — verify fix doesn't break anything
5. **Get emergency approval** — Architect role approves
6. **Create hotfix tag** — `vX.Y.Z-hotfix.N`
7. **Deploy hotfix** — immediate deployment
8. **Create proper patch release** — merge hotfix into main, create PATCH release
9. **Document in ENGINEERING_HISTORY.md** — record what happened and why

### Hotfix Rules

- Hotfixes are exceptional, not routine
- Must be followed by proper PATCH release
- Hotfix branches are deleted after merge
- All hotfixes require post-mortem in ENGINEERING_HISTORY.md


---

## End of Document

This document defines the release procedures for the Agent Developer project.

It is the authoritative reference for:
- Release types (major, minor, patch, hotfix)
- Versioning scheme (Semantic Versioning)
- Release workflow (preparation, verification, release, post-release)
- Pre-release checklist (code quality, documentation, build, approval)
- Post-release actions (monitoring, feedback, lessons learned)
- Hotfix procedure (emergency fixes)

All releases must conform to the procedures defined herein.


---

## End of Document

This document defines the release procedures for the Agent Developer project.

It is the authoritative reference for:
- Release types (major, minor, patch, hotfix)
- Versioning scheme (Semantic Versioning)
- Release workflow (preparation, verification, release, post-release)
- Pre-release checklist (code quality, documentation, build, approval)
- Post-release actions (monitoring, feedback, lessons learned)
- Hotfix procedure (emergency fixes)

All releases must conform to the procedures defined herein.

