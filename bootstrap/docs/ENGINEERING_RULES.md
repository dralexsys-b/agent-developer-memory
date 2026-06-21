# Engineering Rules

Canonical engineering rules for the Agent Developer project ecosystem.
All repositories (Runtime, Agents, Plugins, UI) must follow these rules.

## Core Principles

### Rule -1: Architecture serves implementation
> Архитектура существует для упрощения реализации, а не реализация для подтверждения архитектуры.
If an architectural decision complicates code without tangible benefit, the architecture must change.

### Rule 0: Prefer simple architecture over complex implementation
> Предпочитай простую архитектуру сложной реализации.
Better to add a small class than an `if` statement. Better to add a package than a new responsibility to an existing class. Explicit dependencies are better than magical behavior.

### Rule 1: Structure follows implementation
> Structure follows implementation, not anticipation.
No new directories are created in advance. A directory appears only together with the first working implementation.

### Rule 2: Scripts become files
> Любой shell-скрипт, который выполняется больше одного раза, становится файлом в репозитории.
Scripts do not live in chat history. They live in `scripts/`.

### Rule 3: Bootstrap isolation
> Bootstrap никогда не импортирует Runtime.
Dependency direction: `bootstrap → runtime` (at creation time). Never the reverse.

## Code Quality Rules

- **No `Any`** without explicit justification.
- **No `Dict`** instead of a domain model.
- **No `Optional`** without a clear reason.
- **All public APIs** must be fully typed.
- **Project must pass `mypy --strict` with zero errors.**
- **ruff** is mandatory for linting and formatting.
- **pytest** is mandatory. Every new public class must be accompanied by a test.
- **No global state**.
- **No `# type: ignore`** without a comment explaining the reason.
- **Absolute imports** only (e.g., `from agent_runtime.domain import Task`, never `from .domain import Task`).
- **Explicit `__all__`** in every `__init__.py`.
- **Docstrings** are mandatory for all public methods and classes.

## Process Rules

- **Development Cycle:** Roadmap → Implementation → Tests → Review → Lessons → Architecture Update (only if strictly necessary).
- **Code refutes architecture:** Code has the right to refute an architectural hypothesis, but only after Review and with the reason recorded in `DECISIONS.md`.
- **No technical debt in Foundation:** Phase 0 must not contain `TODO`, `FIXME`, or "temporary solutions". Better to implement less, but completely.
- **Contracts first:** Contracts must be written before implementation.
- **No God Objects:** If a file grows too large, create a new service instead of adding more methods.
- **Event Bus is transport:** Bus only knows about events, subscribers, and delivery. It knows nothing about Domain or Runtime.
- **Registry is a catalog:** Registry only answers register/get/list/has. It does not create, configure, or initialize objects.
- **Layer dependencies:** Each layer only knows the next layer down (Application → Runtime → Contracts → Domain → Kernel). No upward imports.
- **Review is mandatory:** Between Tests and Lessons, a Review stage is required to decide if architecture needs changing or if only code needs fixing.
