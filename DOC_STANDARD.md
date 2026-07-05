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

## Documentation Principles

Documentation standards ensure that engineering knowledge remains consistent, maintainable, and verifiable throughout the project lifecycle.

Core principles:

1. **Canonical Source** — every engineering fact has exactly one authoritative location; other documents reference it rather than duplicate
2. **Living documents** — documentation must reflect current state of the project; outdated documentation is worse than missing documentation
3. **Explicit scope** — each document answers a specific primary question and declares its boundaries
4. **Declared dependencies** — relationships between documents are explicit (Dependencies and Dependents fields), not assumed
5. **Verification friendly** — documentation should be structured to enable automated verification where practical
6. **Minimal duplication** — derived information references canonical source rather than copying; changes propagate through references

Documentation is versioned, reviewed, maintained, and verified with the same engineering rigor as code.

**Engineering Invariant:** Documentation is an engineering artifact, not a byproduct.



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

## Engineering Statement Properties

Engineering documentation is composed of engineering statements that describe systems, processes, requirements, constraints, decisions, or other engineering knowledge. High-quality engineering statements exhibit the following properties.

### Explicit

- All assumptions, constraints, and conditions should be stated explicitly
- Statements that depend on external context should reference that context

### Consistent

- Engineering statements should not contradict canonical sources or other statements within their declared scope

### Verifiable

- Engineering statements should be stated in a way that allows verification whenever verification is reasonably applicable
- When a statement is not directly verifiable, its nature (for example, an assumption or planned change) should be stated explicitly

### Scoped

- Every engineering statement operates within a declared scope
- Statements must not make claims beyond their documented scope without explicit qualification

### Referenced

- Engineering statements should reference the canonical source whenever the statement is derived from another engineering artifact
- Derived statements should reference rather than duplicate canonical content

### Relationship to Documentation Principles

Engineering Statement Properties support the Documentation Principles by improving clarity, consistency, and verification of engineering documentation.

**Engineering Invariant:** Engineering statements are explicit, consistent, and verifiable within their documented scope.

---

## Shell Command Documentation

Engineering documentation frequently contains shell commands. Such commands must be documented so they can be executed safely, reproduced consistently, and understood without additional context.

### Reproducibility

- Commands must be deterministic: given the same initial state, they produce the same result
- Document prerequisites explicitly (required tools, environment variables, directory structure)
- Avoid commands that depend on transient state (timestamps, random values, external services) unless explicitly noted
- Reference the canonical document instead of duplicating long command sequences when appropriate

### Safety

- Potentially destructive or system-modifying commands should explicitly state their effects
- Commands requiring elevated privileges must explicitly indicate this (e.g., `sudo`, `#` prompt)
- Commands that may modify or remove data, system state, or infrastructure should be clearly identified and accompanied by appropriate warnings

### Command Presentation

- When prompts are shown, use consistent prompt indicators: `$` for user commands, `#` for root commands
- For copy/paste blocks, omit prompt prefixes to prevent execution errors
- Use `\` for line continuation with 2-space indentation on continuation lines
- Use `bash` as the default language identifier for shell command blocks; use `sh` only when shell portability is intentional

### Copy/Paste Considerations

- Replace user-specific values with explicit placeholders (e.g., `<PROJECT_DIR>`, `<BRANCH_NAME>`)
- Document any required manual or interactive steps explicitly
- If a command requires interactive input, document this explicitly before the command block

### Executability

Executability is a property of instructional documentation, not a universal requirement for all documents. When documentation contains executable instructions intended to be followed by the reader:

- The sequence must form a complete procedure with no implicit steps or unstated assumptions
- Each instruction must be valid in the documented context (working directory, environment, system state)
- Transitions between steps must preserve the expected state without requiring undocumented manual actions
- Document the expected outcome so successful execution can be verified

Executability complements reproducibility and copy/paste safety by ensuring that executable procedures are complete, self-contained, and verifiable.

### Relationship to Documentation Standards

Shell command documentation is an engineering artifact. It is subject to the same documentation standards, verification practices, and quality requirements as every other part of the document.

**Engineering Invariant:** Documented shell commands must be reproducible, understandable, and safe to execute within their documented context.

---

## Heredoc Documentation

Heredoc syntax is used when documentation embeds another artifact (configuration file, script, data structure) whose formatting and structure are significant to the resulting engineering artifact.

### When to Use Heredoc

- Use heredoc when embedding multi-line content whose structure or readability should be preserved
- Use heredoc when the content will be written to a file or passed as input to a command

### Delimiter Selection

- Prefer descriptive delimiters when they improve readability (e.g., `YAML_EOF`, `CONFIG_EOF`, `SCRIPT_EOF`)
- Use quoted delimiters (`'EOF'`) when the content must not undergo variable expansion
- Use unquoted delimiters (`EOF`) only when variable expansion is intentional and documented

### Embedded Content

- Preserve the formatting of the embedded artifact exactly as it is intended to appear after execution
- Document the content type and expected format before the heredoc block
- Use explicit placeholders for sensitive values (passwords, tokens, secrets) and document the substitution requirement
- Ensure the closing delimiter appears on its own line with no trailing content

### Relationship to Shell Command Documentation

Heredoc documentation is a specialized form of shell command documentation used for embedded engineering artifacts. The same engineering principles apply: reproducibility, safety, and clarity. Heredocs are subject to the same verification and quality requirements as shell commands.

**Engineering Invariant:** A documented heredoc must preserve the intended content of the embedded engineering artifact and remain reproducible within its documented execution context.

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

## Documentation Conformance

A document conforms to this standard when it satisfies all mandatory requirements defined by this document.

### Conformance Criteria

Conformance requires all of the following:

- Required structural elements are present (metadata, headings, sections)
- Metadata is complete and follows the specified format
- Formatting follows the rules defined in this standard
- Cross-references conform to project naming and linking rules
- Engineering statements satisfy the documented statement properties
- Specialized documentation elements (for example, shell commands and heredocs) satisfy their applicable documentation rules

### Non-conformance

If any mandatory requirement defined by this standard is violated, the document is non-conforming until the violation is corrected.

### Relationship to Other Documents

Documentation Conformance defines the expected state of documentation.

The processes used to assess or enforce conformance are defined by their own canonical documents and are intentionally outside the scope of this standard.

**Engineering Invariant:** A document either conforms to this standard or is identified as non-conforming.

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

