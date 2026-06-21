# Bootstrap

Shared templates, scripts, and engineering standards for all Agent Developer repositories.

## Purpose

Bootstrap is the single source of truth for:
- Repository templates (README, .gitignore, pyproject.toml, etc.)
- Engineering scripts (smoke tests, checks, bootstrap automation)
- Engineering documentation (rules, decisions, architecture patterns)
- Examples for each implementation phase

## Rule 3

> Bootstrap never imports Runtime. Runtime may use Bootstrap only during repository creation.

Dependency direction:

    bootstrap → runtime (at creation time)
    runtime ⤬ bootstrap (never)

## Structure

- `templates/` — reusable file templates (README, .gitignore, pyproject.toml, etc.)
- `scripts/` — engineering scripts (bootstrap-layout.sh, smoke.sh, check.sh, etc.)
- `docs/` — engineering documentation (ARCHITECTURE.md, ENGINEERING_RULES.md, DECISIONS.md, IMPLEMENTATION_LOG.md)
- `examples/` — phase-specific examples (phase0/, phase1/, etc.)

## Usage

When creating a new repository (e.g., `agent-developer-runtime`):

    # Copy templates
    cp bootstrap/templates/README.md /path/to/new-repo/README.md
    cp bootstrap/templates/gitignore /path/to/new-repo/.gitignore
    
    # Run bootstrap script
    bootstrap/scripts/bootstrap-layout.sh

After repository creation, the new repository should NOT depend on bootstrap.
