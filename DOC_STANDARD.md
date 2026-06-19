# Documentation Standard

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-18  
**Authority:** Documentation Lead  
**Maintainer:** Documentation Maintainer  

**Type:** Standard (Layer 3: Engineering Knowledge)  
**Primary Question:** "How do we write documentation?"  
**Canonical Source for:** Documentation formatting, structure, naming conventions, quality requirements  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, ENGINEERING_PLAYBOOK.md  
**Dependents:** RELEASE_PROCESS.md, AUTOMATION.md, ENGINEERING_HISTORY.md  

---

## Document Requirements

Every document in the project must satisfy the following requirements:

### Mandatory Elements

1. **Metadata header** — all required fields present (see Metadata Requirements)
2. **End of Document section** — summary and authoritative statement
3. **Dependencies field** — list documents this document reads (even if empty)
4. **Dependents field** — list documents that read this document (even if empty)

### Scope Boundary

Each document must declare its scope through Primary Question and Canonical Source fields.


---

## Formatting Rules

The following rules are specific to this project. Basic Markdown syntax is assumed.

### Headings

- Exactly one H1 (`#`) per document — the document title
- Do not exceed H4 (`####`) — avoid deeper nesting
- Add blank line before and after headings
- Use `---` separator between main sections (##)

### Spacing

- Mandatory blank line after metadata header
- Mandatory blank line before and after lists, tables, code blocks
- Mandatory blank line between paragraphs

### Tables

- Use consistent column alignment
- Add blank line before and after tables
- Keep tables readable — avoid very long cells

### Lists

- Use `-` for unordered lists
- Use `1.` for ordered lists
- Indent nested lists with 2 spaces

### Code Blocks

- Specify language after triple backticks (e.g., ```bash, ```python)
- Use inline code with single backticks for short snippets


---

## Metadata Requirements

Every document must include the following metadata in the header:

### Required Fields

| Field | Description | Example |
|-------|-------------|---------|
| **Status** | Current status of the document | `ACCEPTED`, `DRAFT`, `DEPRECATED` |
| **Version** | Version number | `1.0`, `2.1` |
| **Date** | Last modification date | `2026-06-18` |
| **Authority** | Role that approves the document | `Project Architect`, `Engineering Lead` |
| **Maintainer** | Role that updates the document | `Documentation Maintainer`, `Engineering Maintainer` |
| **Type** | Document type | `Protocol`, `Standard`, `Playbook`, `Architecture`, `Index`, `Registry`, `History`, `Context` |
| **Primary Question** | Main question the document answers | `"What is this project?"`, `"How do we develop this project?"` |
| **Canonical Source for** | What facts this document owns | `Engineering Principles, Roles, Source of Truth hierarchy` |
| **Dependencies** | Documents this document reads | `INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md` |
| **Dependents** | Documents that read this document | `DOC_STANDARD.md, RELEASE_PROCESS.md` |

### Optional Fields

| Field | Description | Example |
|-------|-------------|---------|
| **Lifecycle** | How often the document changes | `Static`, `Semi-static`, `Dynamic`, `Immutable` |

### Formatting

- Use `**Field:**` format for metadata
- Separate metadata from content with `---`
- Use consistent order: Status, Version, Date, Authority, Maintainer, Type, Primary Question, Canonical Source, Dependencies, Dependents
- Do not translate field names (keep in English)


---

## Naming Conventions

### File Names

- Use `UPPER_SNAKE_CASE.md` for document names
- Examples: `PROJECT_PROTOCOL.md`, `ENGINEERING_PLAYBOOK.md`, `DOC_STANDARD.md`
- Use lowercase for directory names: `evidence/`, `adr/`, `logs/`

### Section Names

- Use `Title Case` for main section headings (##)
- Use `Sentence case` for subsection headings (###, ####)
- Be descriptive but concise
- Avoid special characters in headings

---

## Cross-references

### Linking to Other Documents

- Use relative paths: `[text](DOCUMENT.md)`
- Use repository-relative paths for cross-repository links
- Do not use absolute filesystem paths

### Linking to Sections

- Use anchors: `[text](#section-name)`
- Convert section names to lowercase
- Replace spaces with hyphens
- Remove special characters

Example (using 4-space indent for code block):

    ## Development Workflow
    ...
    See [Phase 1: Planning](#phase-1-planning) for details.

### Linking to Evidence

- Use relative paths to evidence files
- Evidence filenames follow project naming convention: `YYYY-MM-DD_HHMM_description.log`
- Example: `[evidence/2026-06-18_1430_test.log](evidence/2026-06-18_1430_test.log)`


---

## Document Quality Checklist

Before committing any document, verify the following:

### Structural Requirements

- [ ] Metadata header complete (all required fields present)
- [ ] Fields in correct order (Status, Version, Date, Authority, Maintainer, Type, Primary Question, Canonical Source, Dependencies, Dependents)
- [ ] Exactly one H1 heading (document title)
- [ ] End of Document section exists
- [ ] Dependencies field present (even if empty)
- [ ] Dependents field present (even if empty)
- [ ] Primary Question field present
- [ ] Canonical Source field present

### Formatting Requirements

- [ ] Heading hierarchy valid (no headings deeper than H4)
- [ ] Blank lines present between sections
- [ ] Tables formatted consistently (proper alignment, separators)
- [ ] Code blocks specify language
- [ ] Lists use consistent style (- for unordered, 1. for ordered)
- [ ] `---` separators between main sections (##)

### References Requirements

- [ ] All links use relative paths (no absolute filesystem paths)
- [ ] All internal references follow project format (lowercase, hyphens, no special chars)
- [ ] Evidence paths follow project naming convention (YYYY-MM-DD_HHMM_description.log)
- [ ] Section anchors follow naming rules (lowercase, hyphens, no special chars)


---

## Examples

### Example 1: Correct Document Header

    # Documentation Standard

    **Status:** ACCEPTED  
    **Version:** 1.0  
    **Date:** 2026-06-18  
    **Authority:** Documentation Lead  
    **Maintainer:** Documentation Maintainer  

    **Type:** Standard (Layer 3: Engineering Knowledge)  
    **Primary Question:** "How do we write documentation?"  
    **Canonical Source for:** Documentation formatting, structure, naming conventions, quality requirements  
    **Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md  
    **Dependents:** RELEASE_PROCESS.md, AUTOMATION.md

    ---

### Example 2: Correct Table Format

    | Column 1 | Column 2 | Column 3 |
    |----------|----------|----------|
    | Value 1  | Value 2  | Value 3  |
    | Value 4  | Value 5  | Value 6  |

### Example 3: Correct List Format

    - List item 1
    - List item 2
      - Nested item
      - Another nested item
    - List item 3

    1. Ordered item 1
    2. Ordered item 2
    3. Ordered item 3

### Example 4: Correct Code Block

    cd ~/agent-dev/proj_memory_arch
    git status
    git log --oneline -5

### Example 5: Correct Cross-reference

    For detailed procedures, see [ENGINEERING_PLAYBOOK.md](ENGINEERING_PLAYBOOK.md).

    See [Phase 1: Planning](#phase-1-planning) for details.

    Evidence: [evidence/2026-06-18_1430_test.log](evidence/2026-06-18_1430_test.log)

---

## End of Document

This document defines the documentation standards for the Agent Developer project.

It is the authoritative reference for:
- Document requirements (mandatory elements, scope boundary)
- Formatting rules (project-specific)
- Metadata requirements (required and optional fields)
- Naming conventions (file names, section names)
- Cross-reference guidelines (linking to documents, sections, evidence)
- Document quality checklist (verifiable requirements before commit)

All documentation must conform to the standards defined herein.

