# Agent Developer Memory

Архитектурная документация для системы Agent Developer — автономного AI-агента для разработки программного обеспечения.

## 📋 О проекте

**Agent Developer Memory** — это репозиторий, содержащий архитектурную документацию, определяющую структуру, поведение и реализацию системы Agent Developer.

Система предназначена для:
- Автоматической разработки программного обеспечения по требованиям пользователя
- Непрерывного обучения на основе выполненных задач
- Управления знаниями, навыками и архитектурными решениями
- Координации множества специализированных агентов

## 🏗️ Архитектура

Документация организована в три слоя:

### Layer 1 — Information Architecture
Определяет организацию информации и структуру памяти.

- **INFORMATION_ARCHITECTURE.md** — мета-архитектура всей системы

### Layer 2 — Operational Architecture ✅ COMPLETED
Определяет доменную модель, границы системы и жизненный цикл задач.

- **PROJECT_PROTOCOL.md** — протокол проекта, роли, правила работы
- **DOMAIN_ARCHITECTURE.md** — доменная модель (сущности, контракты, состояния, события)
- **SYSTEM_BOUNDARIES.md** — границы системы (сервисы, runtime, storage, проекции)
- **TASK_LIFECYCLE.md** — жизненный цикл задачи (13 этапов от Input до Learning)

### Layer 3 — Runtime Implementation 🚧 PLANNED
Определяет реализацию исполняемой системы.

- Runtime Engine
- FSM / State Machine
- Agent Runtime
- Memory Engine
- Execution Engine
- Context Manager
- Capability Resolver
- Event Bus

## 📚 Основные документы

### PROJECT_PROTOCOL.md
Определяет идентичность проекта, роли (Project Architect, Engineering Maintainer), правила работы с документацией и процесс принятия решений.

### DOMAIN_ARCHITECTURE.md
Доменная модель системы, включающая:
- **Сущности:** Portfolio, Project, Task, Workspace, Artifact, Decision, Skill, Tool, Knowledge Item, Release
- **Контракты:** обязательные поля для каждой сущности
- **Состояния:** FSM для Task, Artifact, Decision, Release
- **События:** Event Model с source/target
- **Роли:** Architect, Planner, Coder, Reviewer, Integrator, Learning

**Ключевой принцип:** Architecture Law #1 — доменная модель независима от реализации (runtime, storage, orchestration).

### SYSTEM_BOUNDARIES.md
Определяет, как доменные сущности обслуживаются:
- **Services:** Knowledge Service, Memory Service, Learning Service, Search Service, Registry Service (facade), Execution Service
- **Runtime:** Runtime Session, Execution Context, Queues, Caches, Agents
- **Storage:** Markdown, JSON, SQLite, Qdrant, Git
- **Projections:** Document как форма представления

**Ключевые решения:**
- Registry Service — фасад над SkillRegistry, ToolRegistry, ReleaseRegistry
- Execution Service принимает Tool объект (не зависит от Registry)
- Агенты реализуют роли из доменной модели

### TASK_LIFECYCLE.md
Определяет полный жизненный цикл задачи пользователя (13 этапов):

    Stage 0: Input → Raw Requirements
    Stage 1: Requirements Analysis + Knowledge Retrieval → Requirements Report
    Stage 2: Clarification → Clarified Requirements
    Stage 3: Technical Specification + Constraints + Acceptance Criteria → Engineering Spec
    Stage 4: Architecture + Decision Records → Architectural Decisions
    Stage 5: Project Planning + Implementation Plan → Project Structure
    Stage 6: Capability Resolution → Capability Map
    Stage 7: Development → Working Code
    Stage 8: Integration → Integrated Project
    Stage 9: Engineering Review → Review Package
    Stage 10: User Approval → Approved Changes
    Stage 11: Release / Delivery (Optional) → Released Product
    Stage 12: Learning Consolidation → Lessons Learned

**7 Core Principles:**
1. Task is Primary Object
2. Documentation First
3. Human Approval
4. Continuous Learning
5. Code is Middle
6. Failure is Terminal Outcome
7. Release is Optional

## 🎯 Принципы проекта

### Architecture Law #1
> Если сущность перестаёт существовать при замене runtime, orchestration engine или storage, то она не принадлежит Domain Architecture.

Это обеспечивает независимость доменной модели от реализации и позволяет заменять компоненты без изменения архитектуры.

### Four-Level Architecture
1. **Domain Architecture** — вечные сущности (не меняются)
2. **System Boundaries** — сервисы (могут меняться)
3. **Runtime** — исполнение (может меняться)
4. **Storage** — носители (могут меняться)

### Continuous Documentation
Документация обновляется после каждого этапа жизненного цикла задачи, обеспечивая непрерывное обновление памяти проекта.

## 🗺️ Roadmap

### ✅ Completed

**Layer 1 — Information Architecture**
- [x] INFORMATION_ARCHITECTURE.md

**Layer 2 — Operational Architecture**
- [x] PROJECT_PROTOCOL.md
- [x] DOMAIN_ARCHITECTURE.md
- [x] SYSTEM_BOUNDARIES.md
- [x] TASK_LIFECYCLE.md

### 🚧 In Progress

**Layer 3 — Runtime Implementation**
- [ ] LAYER3_ROADMAP.md
- [ ] Runtime Engine
- [ ] FSM / State Machine
- [ ] Agent Runtime
- [ ] Context Manager
- [ ] Memory Engine
- [ ] Execution Engine
- [ ] Capability Resolver
- [ ] Orchestrator
- [ ] Event Bus

## 📊 Статус проекта

**Текущий этап:** Layer 2 — Operational Architecture ✅ COMPLETED

**Завершённые документы:**
- PROJECT_PROTOCOL.md (протокол проекта)
- DOMAIN_ARCHITECTURE.md (доменная модель, ~1100 строк)
- SYSTEM_BOUNDARIES.md (границы системы, ~1070 строк)
- TASK_LIFECYCLE.md (жизненный цикл задачи, ~1200 строк)

**Следующий шаг:** Layer 3 — Runtime Implementation

## 🔧 Технологии

- **LLM:** Qwen (через llama.cpp)
- **Runtime:** Dual AMD Radeon VII (ROCm)
- **Storage:** Markdown, JSON, SQLite, Qdrant
- **Version Control:** Git
- **Repository Structure:** Layered architecture (Layer 1 → Layer 2 → Layer 3)

## 📝 Лицензия

Этот репозиторий содержит архитектурную документацию и не включает исполняемый код.

## 🤝 Вклад

Этот проект находится в активной разработке. Архитектурные решения принимаются через процесс, описанный в PROJECT_PROTOCOL.md.

---

**Последнее обновление:** 2026-06-21  
**Статус:** Layer 2 Completed, Layer 3 Planned
