# Domain Architecture

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-21  
**Authority:** Project Architect  
**Maintainer:** Architecture Maintainer  

**Type:** Architecture (Layer 2: Operational Knowledge)  
**Primary Question:** "Какова архитектура предметной области системы?"  
**Canonical Source for:** Domain entities, contracts, relationships, state models, event model  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md  
**Dependents:** SYSTEM_BOUNDARIES.md, TASK_LIFECYCLE.md, все будущие runtime-компоненты  
**Lifecycle:** Semi-static (может изменяться по мере эволюции системы)

---

## Purpose

Этот документ определяет архитектуру предметной области системы Agent Developer.

Доменная архитектура — это метамодель всей системы. Она описывает основные сущности, их связи и контракты.

Все будущие компоненты (Task Lifecycle, FSM, LangGraph, Tools, Memory) будут реализовывать эту модель.

### Architecture Law #1

> *See Architecture Law #1 in Purpose section.*

This law guarantees that domain architecture remains stable regardless of implementation evolution.


Этот закон автоматически определяет границы доменной модели:

**Принадлежат Domain Architecture:**
- Task — существует независимо от того, кто её выполняет
- Decision — существует независимо от того, где хранится
- Artifact — существует независимо от формата представления
- Skill — существует независимо от того, как используется
- Knowledge Item — существует независимо от способа поиска
- Event — существует независимо от механизма доставки
- State — существует независимо от FSM engine

**Не принадлежат Domain Architecture:**
- Agent — runtime-исполнитель (заменяется на другой агент)
- Runtime Session — runtime-контекст (исчезает при stateless execution)
- Registry — сервис хранения (заменяется другим хранилищем)
- Memory Service — сервис агрегации (заменяется другим механизмом)
- Markdown, JSON, SQLite, Qdrant, Git — storage (заменяется другим носителем)
- LangGraph, FSM engine — runtime (заменяется другим orchestrator)

### Разделение на четыре уровня

Архитектура системы разделена на четыре независимых уровня:

**Уровень 1: DOMAIN ARCHITECTURE (вечные сущности)**
- Portfolio, Project, Task, Workspace
- Artifact, Decision, Skill, Tool, Knowledge Item, Release
- Event, State, Role
- Почти никогда не меняется
- Фундамент системы

**Уровень 2: SYSTEM BOUNDARIES (сервисы)**
- Knowledge Service, Memory Service, Learning Service
- Search Service, Registry Service, Execution Service
- Описывается в SYSTEM_BOUNDARIES.md

**Уровень 3: RUNTIME (исполнение)**
- Runtime Session, Execution Context
- Queues, Caches, Agents
- Реализуют Role из доменной модели
- Описывается в runtime-документах

**Уровень 4: STORAGE (носители)**
- Markdown, JSON, SQLite, Qdrant, Git
- Формы представления сущностей
- Описывается в SYSTEM_BOUNDARIES.md

Это разделение позволяет:
- Стабилизировать фундамент (Domain Architecture не зависит от реализации)
- Заменять реализацию без изменения сущностей
- Избежать смешения понятий

### Почему Domain Architecture, а не Domain Model?

Этот документ содержит не только сущности, но и:
- Контракты сущностей
- Отношения между сущностями
- State Models (FSM)
- Event Model
- Role Model

Это архитектура предметной области, а не просто список сущностей.

---

## Core Entities Hierarchy

    Portfolio
        │
        ▼
    Project
        │
        ├── Task
        │      │
        │      ├── Workspace
        │      │      │
        │      │      ├── Artifact
        │      │      └── Decision
        │      │
        │      └── Knowledge Items (через Knowledge Service)
        │
        ├── Architecture Model
        └── Release History

### Entity Categories

**Core Entities:**
- Portfolio — контейнер для проектов
- Project — контейнер для задач
- Task — единица работы
- Workspace — изолированное пространство задачи

**Knowledge Entities:**
- Knowledge Item — единица знания
- Skill — навык (как умеем решать)
- Tool — инструмент (чем выполняем)

**Process Entities:**
- Artifact — результат этапа
- Decision — архитектурное решение
- Event — событие системы
- State — состояние сущности
- Release — выпущенная версия

**Role Entities:**
- Role — роль исполнителя (Architect, Planner, Coder, Reviewer, Integrator, Learning)


---

## Portfolio Model

Portfolio — это контейнер для проектов.

Portfolio является владельцем:
- Списка проектов
- Общей стратегии
- Общих ресурсов

### Portfolio Contract

    {
      "id": "portfolio-2026-06-18-restaurant-platform",
      "name": "Restaurant Platform",
      "description": "Платформа для управления ресторанами",
      "created_at": "2026-06-18T10:00:00Z",
      "updated_at": "2026-06-18T14:30:00Z",
      "owner": "user@example.com",
      "status": "ACTIVE",
      "projects": [
        "project-android-app",
        "project-ios-app",
        "project-kitchen-panel",
        "project-courier-app"
      ]
    }

### Portfolio Fields

- **id** — уникальный идентификатор портфолио
- **name** — название портфолио
- **description** — описание портфолио
- **created_at** — время создания
- **updated_at** — время последнего обновления
- **owner** — владелец портфолио
- **status** — статус портфолио (ACTIVE, ARCHIVED, COMPLETED)
- **projects** — список проектов

### Portfolio Lifecycle

Portfolio может находиться в следующих состояниях:
- **ACTIVE** — портфолио активно
- **ARCHIVED** — портфолио архивировано
- **COMPLETED** — портфолио завершено

---

## Project Model

Project — это контейнер для задач.

Project владеет **ссылками** на сервисы и сущности. Реальные владельцы — отдельные сущности и сервисы.

### Project Contract

    {
      "id": "project-2026-06-18-android-app",
      "portfolio_id": "portfolio-2026-06-18-restaurant-platform",
      "name": "Android App",
      "description": "Android-приложение для клиентов",
      "created_at": "2026-06-18T10:00:00Z",
      "updated_at": "2026-06-18T14:30:00Z",
      "owner": "user@example.com",
      "status": "ACTIVE",
      "tasks": ["task-001", "task-002", "task-003"],
      "architecture_ref": "projects/android-app/architecture.md",
      "project_memory_ref": "services/memory-service/android-app",
      "skill_registry_ref": "services/registry-service/skills/android-app",
      "tool_registry_ref": "services/registry-service/tools/android-app",
      "knowledge_base_ref": "services/knowledge-service/android-app",
      "release_registry_ref": "services/registry-service/releases/android-app"
    }

### Project Fields

- **id** — уникальный идентификатор проекта
- **portfolio_id** — идентификатор портфолио
- **name** — название проекта
- **description** — описание проекта
- **created_at** — время создания
- **updated_at** — время последнего обновления
- **owner** — владелец проекта
- **status** — статус проекта (ACTIVE, ARCHIVED, COMPLETED)
- **tasks** — список задач проекта
- **architecture_ref** — ссылка на архитектуру
- **project_memory_ref** — ссылка на Memory Service (сервис)
- **skill_registry_ref** — ссылка на Registry Service для навыков (сервис)
- **tool_registry_ref** — ссылка на Registry Service для инструментов (сервис)
- **knowledge_base_ref** — ссылка на Knowledge Service (сервис)
- **release_registry_ref** — ссылка на Registry Service для релизов (сервис)

### Project Lifecycle

Project может находиться в следующих состояниях:
- **ACTIVE** — проект в разработке
- **ARCHIVED** — проект архивирован
- **COMPLETED** — проект завершён


---

## Task Model

Task — это единица работы в рамках проекта.

Task проходит все этапы жизненного цикла (см. TASK_LIFECYCLE.md).

### Task Contract

    {
      "id": "task-2026-06-18-001",
      "project_id": "project-2026-06-18-android-app",
      "title": "Добавить экран оплаты",
      "source_document": "requirements.pdf",
      "current_stage": 7,
      "status": "IN_PROGRESS",
      "priority": "HIGH",
      "owner": "user@example.com",
      "created_at": "2026-06-18T10:00:00Z",
      "updated_at": "2026-06-18T14:30:00Z",
      "history": [
        {"stage": 0, "timestamp": "2026-06-18T10:00:00Z", "action": "Input received"},
        {"stage": 1, "timestamp": "2026-06-18T10:05:00Z", "action": "Analysis complete"}
      ],
      "artifacts": [
        {"stage": 0, "type": "raw_requirements", "path": "tasks/001/requirements/raw_requirements.pdf"},
        {"stage": 1, "type": "requirements_report", "path": "tasks/001/requirements/requirements_report.md"}
      ],
      "workspace_ref": "tasks/001/"
    }

### Task Fields

- **id** — уникальный идентификатор задачи
- **project_id** — идентификатор проекта
- **title** — название задачи
- **source_document** — исходный документ (PDF, DOCX, etc.)
- **current_stage** — текущий этап (0-12)
- **status** — статус задачи (NEW, ANALYZING, WAITING_USER, PLANNING, IMPLEMENTING, REVIEW, WAITING_APPROVAL, RELEASED, LEARNING, DONE, FAILED)
- **priority** — приоритет (LOW, MEDIUM, HIGH, CRITICAL)
- **owner** — владелец задачи
- **created_at** — время создания
- **updated_at** — время последнего обновления
- **history** — история переходов между этапами
- **artifacts** — список артефактов
- **workspace_ref** — ссылка на workspace

### Task Status

Task может находиться в следующих состояниях (см. State Model):
- **NEW** — задача создана
- **ANALYZING** — анализ требований
- **WAITING_USER** — ожидание ввода от пользователя
- **PLANNING** — планирование
- **IMPLEMENTING** — разработка
- **REVIEW** — ревью
- **WAITING_APPROVAL** — ожидание подтверждения
- **RELEASED** — выпущена
- **LEARNING** — консолидация знаний
- **DONE** — завершена
- **FAILED** — не выполнена

---

## Workspace Model

Workspace — это изолированное пространство задачи.

Каждая задача имеет свой workspace для хранения артефактов, логов, отчётов.

### Workspace Structure

    tasks/
      {task_id}/
        requirements/
          raw_requirements.{ext}
          requirements_report.md
          clarified_requirements.md
          constraints.md
          acceptance_criteria.md
        planning/
          engineering_spec.md
          architecture_decisions.md
          project_manifest.json
          implementation_plan.json
          skill_map.json
          decision_records/
            DR-001-*.md
            DR-002-*.md
        generated/
          lib/
          test/
        reports/
          integration_report.md
          review_package.md
          approval_record.md
          release_notes.md
          lessons_learned.md
        logs/
          stage_0.log
          stage_1.log
        artifacts/
          skill_candidates.json
          quality_metrics.json

### Workspace Purpose

- **Изоляция** — задачи не пересекаются
- **Прослеживаемость** — все артефакты в одном месте
- **Воспроизводимость** — можно восстановить состояние задачи
- **Аудит** — все логи и отчёты сохранены


---

## Artifact Model

Artifact — это результат этапа жизненного цикла.

Каждый артефакт имеет контракт, который позволяет runtime работать с ним единообразно.

### Artifact Contract

    {
      "id": "artifact-2026-06-18-001",
      "type": "requirements_report",
      "task_id": "task-2026-06-18-001",
      "stage": 1,
      "owner_role": "Requirements Analyzer",
      "created_by_role": "Requirements Analyzer",
      "created_at": "2026-06-18T10:05:00Z",
      "version": 1,
      "status": "FINAL",
      "path": "tasks/001/requirements/requirements_report.md",
      "hash": "sha256:abc123...",
      "metadata": {
        "word_count": 1500,
        "requirements_count": 25,
        "gaps_identified": 5
      }
    }

### Artifact Fields

- **id** — уникальный идентификатор артефакта
- **type** — тип артефакта
- **task_id** — идентификатор задачи
- **stage** — этап, на котором создан артефакт
- **owner_role** — роль-владелец
- **created_by_role** — роль-создатель
- **created_at** — время создания
- **version** — версия артефакта
- **status** — статус (DRAFT, FINAL, SUPERSEDED)
- **path** — путь к файлу
- **hash** — хэш содержимого
- **metadata** — дополнительные метаданные

### Artifact Types

**Requirements Artifacts:**
- raw_requirements — исходные требования
- requirements_report — отчёт о анализе требований
- clarified_requirements — уточнённые требования
- constraints — ограничения
- acceptance_criteria — критерии приёмки

**Planning Artifacts:**
- engineering_spec — инженерная спецификация
- architecture_decisions — архитектурные решения
- project_manifest — манифест проекта
- implementation_plan — план реализации
- skill_map — карта навыков

**Development Artifacts:**
- code — исходный код
- integration_report — отчёт об интеграции

**Release Artifacts:**
- review_package — пакет для ревью
- approval_record — запись о подтверждении
- release_notes — заметки о релизе

**Learning Artifacts:**
- lessons_learned — извлечённые уроки
- skill_candidates — кандидаты в навыки
- quality_metrics — метрики качества

### Artifact State

Artifact проходит через следующие состояния:

    DRAFT → IN_REVIEW → APPROVED → FINAL

Переходы:
- **DRAFT → IN_REVIEW**: Trigger = ReviewRequested
- **IN_REVIEW → APPROVED**: Trigger = ReviewApproved
- **APPROVED → FINAL**: Trigger = Published
- **Любое → SUPERSEDED**: Trigger = NewVersionCreated


---

## Decision Model

Decision — это архитектурное решение, принятое на любом этапе жизненного цикла.

Decision Records — это сквозная сущность, которая может создаваться на любом этапе.

### Decision Contract

    {
      "id": "DR-001",
      "task_id": "task-2026-06-18-001",
      "stage": 4,
      "title": "State Management",
      "context": "Нужно выбрать state management для Flutter-приложения",
      "alternatives": ["Riverpod", "BLoC", "Provider"],
      "chosen": "Riverpod",
      "reason": "Более современный подход, лучшая тестируемость, меньше boilerplate",
      "consequences": "Команда должна изучить Riverpod, нужно настроить dependency injection",
      "created_by_role": "Architect",
      "created_at": "2026-06-18T11:00:00Z",
      "status": "APPROVED"
    }

### Decision Fields

- **id** — уникальный идентификатор решения (DR-XXX)
- **task_id** — идентификатор задачи
- **stage** — этап, на котором принято решение
- **title** — название решения
- **context** — контекст (почему нужно решение)
- **alternatives** — список альтернатив
- **chosen** — выбранная альтернатива
- **reason** — обоснование выбора
- **consequences** — последствия выбора
- **created_by_role** — роль, принявшая решение
- **created_at** — время принятия решения
- **status** — статус (PROPOSED, APPROVED, SUPERSEDED)

### Decision State

Decision проходит через следующие состояния:

    PROPOSED → APPROVED → SUPERSEDED

Переходы:
- **PROPOSED → APPROVED**: Trigger = DecisionApproved
- **APPROVED → SUPERSEDED**: Trigger = NewDecisionMade

---

## Skill Model

Skill — это навык, который отвечает на вопрос: **"Как мы умеем решать задачу?"**

Skill — это знание, а не исполнение.

### Skill Contract

    {
      "id": "skill-flutter-ui",
      "name": "Flutter UI",
      "description": "Создание UI-компонентов на Flutter",
      "category": "development",
      "status": "APPROVED",
      "version": "1.0",
      "created_at": "2026-06-18T10:00:00Z",
      "updated_at": "2026-06-18T14:30:00Z",
      "source_task_id": "task-2026-06-18-001",
      "usage_count": 15,
      "success_rate": 0.95,
      "required_tools": ["flutter", "dart"]
    }

### Skill Fields

- **id** — уникальный идентификатор навыка
- **name** — название навыка
- **description** — описание навыка
- **category** — категория (development, testing, documentation, analysis)
- **status** — статус (CANDIDATE, APPROVED, DEPRECATED)
- **version** — версия навыка
- **created_at** — время создания
- **updated_at** — время последнего обновления
- **source_task_id** — источник навыка (task_id)
- **usage_count** — количество использований
- **success_rate** — процент успешных использований
- **required_tools** — список требуемых инструментов

### Skill Lifecycle

Skill может находиться в следующих состояниях:
- **CANDIDATE** — навык предложен, но не одобрен
- **APPROVED** — навык одобрен и может использоваться
- **DEPRECATED** — навык устарел

### Skill Candidate

**Note:** Skill Candidate is a temporary process artifact (subtype of Artifact) that exists until knowledge consolidation (Stage 12). It is not a standalone domain entity.

Skill Candidate — это предложение навыка, созданное на любом этапе.

После консолидации (Stage 12) Skill Candidate становится Skill или отклоняется.

    {
      "id": "candidate-2026-06-18-001",
      "task_id": "task-2026-06-18-001",
      "stage": 7,
      "skill_name": "flutter-repository-pattern",
      "proposed_by_role": "Coder",
      "reason": "Отличный паттерн для работы с данными",
      "status": "PENDING",
      "created_at": "2026-06-18T13:00:00Z"
    }

---

## Tool Model

Tool — это инструмент, который отвечает на вопрос: **"Чем мы выполняем задачу?"**

Tool отличается от Skill:
- **Skill** — это знание (как решать)
- **Tool** — это исполнение (чем выполнять)

### Tool Contract

    {
      "id": "tool-flutter",
      "name": "Flutter CLI",
      "description": "Flutter command-line interface",
      "category": "build",
      "status": "AVAILABLE",
      "version": "3.19.0",
      "executable": "flutter",
      "platforms": ["linux", "macos", "windows"],
      "capabilities": ["build", "test", "run", "analyze"]
    }

### Tool Fields

- **id** — уникальный идентификатор инструмента
- **name** — название инструмента
- **description** — описание инструмента
- **category** — категория (build, test, vcs, deployment, analysis)
- **status** — статус (AVAILABLE, UNAVAILABLE, DEPRECATED)
- **version** — версия инструмента
- **executable** — исполняемый файл
- **platforms** — поддерживаемые платформы
- **capabilities** — возможности инструмента

### Tool Examples

- **flutter** — Flutter CLI
- **dart** — Dart SDK
- **git** — Git VCS
- **adb** — Android Debug Bridge
- **gradlew** — Gradle build tool
- **xcodebuild** — Xcode build tool

### Tool vs Skill

| Aspect | Skill | Tool |
|--------|-------|------|
| **Question** | How to solve? | What to use? |
| **Example** | Flutter UI | flutter CLI |
| **Nature** | Knowledge | Execution |
| **Lifecycle** | Learned | Installed |


---

## Knowledge Item Model

Knowledge Item — это единица знания с метаданными для поиска и использования.

Knowledge Item — это доменная сущность. Task Memory, Project Memory и Knowledge Base — это сервисы агрегации и представления (описываются в SYSTEM_BOUNDARIES.md).

### Knowledge Item Contract

    {
      "id": "knowledge-2026-06-18-001",
      "type": "lesson_learned",
      "project_id": "project-2026-06-18-android-app",
      "task_id": "task-2026-06-18-001",
      "title": "Riverpod требует явного управления lifecycle",
      "content": "При использовании Riverpod необходимо явно управлять lifecycle providers",
      "category": "technical",
      "source_task_id": "task-2026-06-18-001",
      "confidence": 0.95,
      "tags": ["flutter", "riverpod", "lifecycle"],
      "embedding": [0.123, 0.456, 0.789, ...],
      "relations": ["knowledge-2026-06-18-002", "knowledge-2026-06-18-003"],
      "created_at": "2026-06-18T15:00:00Z"
    }

### Knowledge Item Fields

- **id** — уникальный идентификатор знания
- **type** — тип знания (lesson_learned, pattern, metric, benchmark)
- **project_id** — идентификатор проекта
- **task_id** — идентификатор задачи
- **title** — название знания
- **content** — содержание знания
- **category** — категория (technical, process, tool, architecture)
- **source_task_id** — источник знания
- **confidence** — уверенность (0.0-1.0)
- **tags** — теги для поиска
- **embedding** — векторное представление для семантического поиска
- **relations** — связанные знания
- **created_at** — время создания

### Knowledge Item Types

**Lessons Learned:**
- Что сработало хорошо
- Что можно улучшить
- Какие ошибки были допущены

**Patterns:**
- Архитектурные паттерны
- Паттерны кода
- Паттерны тестирования

**Metrics:**
- Code quality metrics
- Test coverage metrics
- Performance metrics

**Benchmarks:**
- Performance benchmarks
- Memory usage benchmarks
- Build time benchmarks

---

## Release Model

Release — это выпущенная версия проекта.

### Release Contract

    {
      "id": "release-2026-06-18-001",
      "project_id": "project-2026-06-18-android-app",
      "version": "1.0.0",
      "type": "major",
      "created_at": "2026-06-18T15:00:00Z",
      "released_at": "2026-06-18T15:30:00Z",
      "tasks_completed": ["task-001", "task-002", "task-003"],
      "commit_hash": "abc123...",
      "tag": "v1.0.0",
      "status": "RELEASED"
    }

### Release Fields

- **id** — уникальный идентификатор релиза
- **project_id** — идентификатор проекта
- **version** — версия (SemVer)
- **type** — тип релиза (major, minor, patch, hotfix)
- **created_at** — время создания
- **released_at** — время выпуска
- **tasks_completed** — список завершённых задач
- **commit_hash** — хэш коммита
- **tag** — git tag
- **status** — статус (DRAFT, RELEASED, DEPRECATED)

### Release State

Release проходит через следующие состояния:

    DRAFT → RELEASED → DEPRECATED

Переходы:
- **DRAFT → RELEASED**: Trigger = ReleasePublished
- **RELEASED → DEPRECATED**: Trigger = NewVersionReleased


---

## Event Model

Event — это событие системы, которое вызывает переход между состояниями.

События являются **глобальными** и могут иметь source и target.

### Event Contract

    {
      "id": "event-2026-06-18-001",
      "type": "RequirementsReceived",
      "timestamp": "2026-06-18T10:00:00Z",
      "source": {
        "type": "user",
        "id": "user@example.com"
      },
      "target": {
        "type": "task",
        "id": "task-2026-06-18-001"
      },
      "payload": {
        "document_path": "tasks/001/requirements/raw_requirements.pdf"
      }
    }

### Event Fields

- **id** — уникальный идентификатор события
- **type** — тип события
- **timestamp** — время события
- **source** — источник события (type, id)
- **target** — цель события (type, id)
- **payload** — данные события

### Event Types

**Input Events:**
- RequirementsReceived — требования получены
- ClarificationAnswered — пользователь ответил на вопросы
- ApprovalGranted — пользователь подтвердил

**Process Events:**
- TaskCreated — задача создана
- AnalysisCompleted — анализ завершён
- PlanningCompleted — планирование завершён
- FileCompleted — файл создан
- IntegrationPassed — интеграция пройдена

**Decision Events:**
- DecisionCreated — решение создано
- DecisionApproved — решение одобрено

**Learning Events:**
- SkillCandidateProposed — навык предложен
- LessonLearned — урок извлечён
- BenchmarkRecorded — benchmark записан

**Release Events:**
- ReleaseCompleted — релиз завершён
- DocumentationUpdated — документация обновлена

**System Events:**
- GitPullFailed — git pull не удался
- ModelRestarted — модель перезапущена
- GPUOutOfMemory — GPU память закончилась
- ToolTimeout — инструмент превысил таймаут
- MemoryUpdated — память обновлена

**Failure Events:**
- TaskFailed — задача не выполнена
- BuildFailed — сборка не удалась
- TestsFailed — тесты не пройдены

### Event Routing

События маршрутизируются по правилам:
- **Source** — кто создал событие
- **Target** — кто должен обработать событие
- **Type** — тип события определяет обработку

---

## State Model

State — это состояние сущности в определённый момент времени.

State Model описывает состояния различных сущностей и переходы между ними.

**Важно:** State Model отвязан от конкретных сущностей. FSM может быть у разных сущностей (Task, Artifact, Decision, Release).

### Task State

Task проходит через следующие состояния:

    NEW
      ↓
    ANALYZING
      ↓
    WAITING_USER ←→ CLARIFYING
      ↓
    PLANNING
      ↓
    IMPLEMENTING ←→ DEVELOPING
      ↓
    REVIEW
      ↓
    WAITING_APPROVAL
      ↓
    RELEASED
      ↓
    LEARNING
      ↓
    DONE

### Task State Transitions

| From | To | Trigger | Condition |
|------|-----|---------|-----------|
| NEW | ANALYZING | RequirementsReceived | Requirements valid |
| ANALYZING | WAITING_USER | ClarificationNeeded | Gaps identified |
| WAITING_USER | CLARIFYING | ClarificationAnswered | All questions answered |
| CLARIFYING | PLANNING | RequirementsClarified | No gaps remaining |
| PLANNING | IMPLEMENTING | PlanningCompleted | Implementation plan ready |
| IMPLEMENTING | DEVELOPING | FileStarted | Skill resolved |
| DEVELOPING | REVIEW | FileCompleted | All files done |
| REVIEW | WAITING_APPROVAL | ReviewCompleted | Review package ready |
| WAITING_APPROVAL | RELEASED | ApprovalGranted | User approved |
| RELEASED | LEARNING | ReleaseCompleted | Release successful |
| LEARNING | DONE | LearningCompleted | Knowledge consolidated |
| Any | FAILED | TaskFailed | Unrecoverable error |

### Task FSM Contract

    {
      "task_id": "task-2026-06-18-001",
      "current_state": "IMPLEMENTING",
      "previous_state": "PLANNING",
      "transition_timestamp": "2026-06-18T12:00:00Z",
      "transition_trigger": "PlanningCompleted",
      "history": [
        {"state": "NEW", "timestamp": "2026-06-18T10:00:00Z"},
        {"state": "ANALYZING", "timestamp": "2026-06-18T10:01:00Z"},
        {"state": "WAITING_USER", "timestamp": "2026-06-18T10:05:00Z"},
        {"state": "CLARIFYING", "timestamp": "2026-06-18T10:15:00Z"},
        {"state": "PLANNING", "timestamp": "2026-06-18T10:30:00Z"},
        {"state": "IMPLEMENTING", "timestamp": "2026-06-18T12:00:00Z"}
      ]
    }

### State Summary

Каждая сущность имеет своё состояние:

| Entity | States |
|--------|--------|
| **Task** | NEW, ANALYZING, WAITING_USER, CLARIFYING, PLANNING, IMPLEMENTING, DEVELOPING, REVIEW, WAITING_APPROVAL, RELEASED, LEARNING, DONE, FAILED |
| **Artifact** | DRAFT, IN_REVIEW, APPROVED, FINAL, SUPERSEDED |
| **Decision** | PROPOSED, APPROVED, SUPERSEDED |
| **Release** | DRAFT, RELEASED, DEPRECATED |
| **Skill** | CANDIDATE, APPROVED, DEPRECATED |
| **Tool** | AVAILABLE, UNAVAILABLE, DEPRECATED |
| **Portfolio** | ACTIVE, ARCHIVED, COMPLETED |
| **Project** | ACTIVE, ARCHIVED, COMPLETED |


---

## Role Model

Role — это роль исполнителя в системе.

**Важно:** Role — это доменная сущность. Agent — это runtime-исполнитель роли (описывается в SYSTEM_BOUNDARIES.md).

### Role Contract

    {
      "id": "role-architect",
      "name": "Architect",
      "description": "Принимает архитектурные решения",
      "capabilities": [
        "analyze_requirements",
        "make_decisions",
        "create_architecture"
      ],
      "allowed_tools": ["flutter", "dart", "git"],
      "allowed_decisions": ["architecture", "technology"],
      "memory_access": {
        "read": ["project_memory", "task_memory", "knowledge_base"],
        "write": ["task_memory", "decision_records"]
      },
      "outputs": ["architecture_decisions", "decision_records"]
    }

### Role Fields

- **id** — уникальный идентификатор роли
- **name** — название роли
- **description** — описание роли
- **capabilities** — возможности роли
- **allowed_tools** — разрешённые инструменты
- **allowed_decisions** — разрешённые решения
- **memory_access** — доступ к памяти (read, write)
- **outputs** — выходные артефакты

### Defined Roles

**Architect:**
- Capabilities: analyze_requirements, make_decisions, create_architecture
- Allowed decisions: architecture, technology
- Outputs: architecture_decisions, decision_records

**Planner:**
- Capabilities: create_plan, estimate_effort, prioritize_tasks
- Allowed decisions: planning, scheduling
- Outputs: implementation_plan, project_manifest

**Coder:**
- Capabilities: write_code, write_tests, fix_bugs
- Allowed decisions: implementation_details
- Outputs: code, tests

**Reviewer:**
- Capabilities: review_code, check_quality, suggest_improvements
- Allowed decisions: quality_approval
- Outputs: review_report, quality_metrics

**Integrator:**
- Capabilities: integrate_code, run_tests, validate_architecture
- Allowed decisions: integration_approval
- Outputs: integration_report

**Learning:**
- Capabilities: extract_lessons, propose_skills, analyze_metrics
- Allowed decisions: skill_approval
- Outputs: lessons_learned, skill_candidates, quality_metrics

---

## Entity Relationships

### Core Relationships

    Portfolio (1) ───── (N) Project
    Project (1) ─────── (N) Task
    Task (1) ────────── (1) Workspace
    Workspace (1) ───── (N) Artifact
    Task (1) ────────── (N) Decision
    Task (1) ────────── (N) Event
    Task (1) ────────── (N) Knowledge Item
    Project (1) ─────── (N) Knowledge Item
    Project (1) ─────── (N) Release

### Knowledge Relationships

    Knowledge Item (N) ←─── (N) Tool (через required_tools в Skill)
    Skill (N) ──────────── (N) Tool (через required_tools)
    Skill (1) ──────────── (N) Skill Candidate

### Role Relationships

    Role (1) ──────────── (N) Decision (через created_by_role)
    Role (1) ──────────── (N) Artifact (через owner_role)
    Role (1) ──────────── (N) Skill Candidate (через proposed_by_role)

### Process Relationships

    Task (1) ──────────── (N) Event
    Event (1) ─────────── (1) State Transition
    State (1) ─────────── (1) FSM
    Decision (1) ──────── (N) Decision Record

---

## Entity Contracts Summary

### Required Fields by Entity

**Portfolio:**
- id, name, owner, status, created_at

**Project:**
- id, portfolio_id, name, owner, status, created_at

**Task:**
- id, project_id, title, current_stage, status, owner, created_at

**Workspace:**
- task_id, path, created_at

**Artifact:**
- id, type, task_id, stage, owner_role, created_at, path, hash

**Decision:**
- id, task_id, stage, title, context, alternatives, chosen, reason, created_at

**Skill:**
- id, name, description, category, status, version, created_at

**Skill Candidate:**
- id, task_id, stage, skill_name, proposed_by_role, reason, status, created_at

**Tool:**
- id, name, description, category, status, version, executable

**Knowledge Item:**
- id, type, project_id, title, content, category, created_at

**Release:**
- id, project_id, version, type, created_at, released_at, status

**Event:**
- id, type, timestamp, source, target

**Role:**
- id, name, description, capabilities, allowed_tools

---

## End of Document

Этот документ определяет архитектуру предметной области системы Agent Developer.

Доменная архитектура — это метамодель всей системы. Она описывает основные сущности, их связи и контракты.

Все будущие компоненты (Task Lifecycle, FSM, LangGraph, Tools, Memory) будут реализовывать эту модель.

### Ключевые принципы

1. **Portfolio is Container** — портфолио является контейнером для проектов
2. **Project is Container** — проект является контейнером для задач и владельцем ссылок
3. **Task is Primary Object** — задача, а не файл, является первичным объектом
4. **Workspace is Isolation** — workspace обеспечивает изоляцию задач
5. **Memory is Aggregated View** — Task/Project Memory это представления Knowledge Items
6. **Decision is Cross-Cutting** — решения могут создаваться на любом этапе
7. **Skill is Knowledge, Tool is Execution** — навыки и инструменты разделены
8. **Role is Domain, Agent is Runtime** — роли в доменной модели, агенты в runtime
9. **Events are Global** — события являются глобальными с source и target
10. **State is Decoupled** — FSM отвязана от конкретных сущностей
11. **Knowledge is Item** — знания являются единицами с embedding и confidence
12. **Document is Projection** — документы это формы представления, не сущности

### Чего нет в этом документе (перенесено в SYSTEM_BOUNDARIES.md)

**System Boundaries (сервисы):**
- Knowledge Service — агрегация знаний
- Memory Service — агрегация Task Memory и Project Memory
- Learning Service — обучение на Knowledge Items
- Search Service — поиск Knowledge Items
- Registry Service — хранение Skill, Tool, Release
- Execution Service — выполнение Tools

**Runtime (исполнение):**
- Runtime Session — контекст выполнения
- Execution Context — состояние исполнения
- Queues — очереди задач
- Caches — кэширование
- Agents — исполнители ролей (Architect Agent, Coder Agent, etc.)

**Storage (носители):**
- Markdown — форма представления Artifact, Decision
- JSON — форма представления контрактов
- SQLite — хранилище сущностей
- Qdrant — векторное хранилище Knowledge Items
- Git — версионирование документов

**Projection (проекции):**
- Document — форма представления любой сущности

### Architecture Law #1

> *See Architecture Law #1 in Purpose section.*

This law guarantees that domain architecture remains stable regardless of implementation evolution.



