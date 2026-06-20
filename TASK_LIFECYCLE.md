# Task Lifecycle

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-21  
**Authority:** Project Architect  
**Maintainer:** Architecture Maintainer  

**Type:** Architecture (Layer 2: Operational Knowledge)  
**Primary Question:** "Как пользовательская задача превращается в готовый программный продукт?"  
**Canonical Source for:** Task lifecycle stages, stage transitions, quality gates, failure paths  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md  
**Dependents:** ENGINEERING_PLAYBOOK.md, все будущие runtime-компоненты  
**Lifecycle:** Semi-static (может изменяться по мере эволюции процесса)

---

## Purpose

Этот документ определяет полный жизненный цикл пользовательской задачи в системе Agent Developer.

Он является контрактом между бизнес-задачей и всеми техническими компонентами системы.

### Почему Task Lifecycle, а не FileState?

FileState описывает жизненный цикл **файла**.
Task Lifecycle описывает жизненный цикл **задачи пользователя**.

Ключевое отличие:
- FileState начинается, когда файл уже существует
- Task Lifecycle начинается, когда пользователь присылает PDF

Разработчик не начинает с кода. Он начинает с понимания задачи.

### Связь с другими документами

- **DOMAIN_ARCHITECTURE.md** — определяет сущности (Task, Artifact, Decision, Knowledge Item, Role)
- **SYSTEM_BOUNDARIES.md** — определяет сервисы (Knowledge Service, Memory Service, Registry Service, Execution Service) и агентов (Architect Agent, Coder Agent, etc.)
- **TASK_LIFECYCLE.md** (этот документ) — определяет этапы и переходы

---

## Core Principles

### 1. Task is Primary Object

Задача (Task) — это первичный объект системы.

Не файл. Не агент. Не инструмент.

Именно Task проходит все стадии. Task имеет состояние, историю, артефакты.

Все компоненты системы служат для продвижения Task от начала до конца.

### 2. Documentation First

Документация не является пассивным архивом.

Она является частью жизненного цикла задачи.

После завершения каждого Stage агент обязан обновить проектную документацию:
- Какие артефакты появились?
- Какие документы изменились?
- Что нужно записать в долговременную память?
- Что должен узнать следующий запуск агента?

Это обеспечивает непрерывное обновление памяти проекта.

### 3. Human Approval

Агент не имеет полномочий выпускать продукт без подтверждения пользователя.

Stage 10 (User Approval) — это точка, где агент останавливается и ждёт.

До этого момента агент может принимать решения, писать код, тестировать.

Но финальное слово всегда за пользователем.

### 4. Continuous Learning

Система должна учиться на каждом завершённом проекте.

Learning — это не только Stage 12 (Learning Consolidation).

Learning начинается с самого начала:
- Stage 1: поиск похожих проектов в памяти
- Stage 7: предложение skill candidates за хорошие паттерны
- Stage 12: консолидация всех знаний

Без этого принципа агент не эволюционирует.

### 5. Code is Middle

Код находится примерно в середине процесса, а не является его центром.

Большинство AI-агентов начинают с генерации кода.

Здесь же код становится лишь одним из этапов реализации задачи.

Процесс:

    Понимание задачи → Анализ → Уточнение → Спецификация → Архитектура → Планирование → [КОД] → Интеграция → Ревью → Approval → Release/Delivery → Learning

Код — это средство, а не цель.

### 6. Failure is Terminal Outcome

Failure — это не отдельное состояние, а терминальный исход любого Stage.

Каждый Stage может завершиться двумя путями:
- **Success** → переход к следующему Stage
- **Failure** → Task status → FAILED

Это упрощает модель FSM и соответствует DOMAIN_ARCHITECTURE.md.

### 7. Release is Optional

Не каждая задача заканчивается релизом.

Stage 11 (Release / Delivery) — опциональный этап.

Задача может быть:
- Библиотекой (не требует релиза)
- Прототипом (не требует релиза)
- Архитектурным документом (не требует релиза)
- Исследованием (не требует релиза)
- Продуктом (требует релиза)

Агент определяет, требуется ли релиз, на основе типа задачи.


---

## Lifecycle Overview

Task Lifecycle состоит из 13 этапов (Stage 0-12):

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
    Stage 11: Release / Delivery (optional) → Released Product
    Stage 12: Learning Consolidation → Lessons Learned

Каждый этап имеет:
- **Input** — что поступает на вход
- **Process** — что делает агент
- **Output** — что является результатом
- **Artifact** — какой артефакт создаётся
- **Quality Gate** — критерий завершения
- **Agent Role** — какая роль задействована
- **Documentation Update** — что обновляется в документации
- **Failure Outcome** — что происходит при неудаче (Task → FAILED)

---

## Stage 0: Input

### Input
- PDF
- DOCX
- Markdown
- Plain text
- Устное описание

### Process
Агент принимает входной материал от пользователя.

### Output

    Raw Requirements

### Artifact Created

    tasks/{task_id}/requirements/raw_requirements.{ext}

### Quality Gate
- Материал принят
- Формат распознан
- Содержание доступно для анализа

### Agent Role
Input Receiver

### Documentation Update
- Task создан в системе
- Workspace создан
- CURRENT_CONTEXT.md обновлён

### Failure Outcome
- Если материал не распознан → Task → FAILED

---

## Stage 1: Requirements Analysis + Knowledge Retrieval

### Input
- Raw Requirements (из Stage 0)

### Process
Агент читает документ и отвечает только на вопросы:
- Что хочет заказчик?
- Что непонятно?
- Что противоречиво?
- Чего не хватает?

**И одновременно** агент ищет в памяти проекта (через Knowledge Service):
- Похожие проекты
- Похожие ТЗ
- Похожие решения

Чтобы понимать: "мы это уже когда-то делали".

**Никакого кода. Вообще.**

### Output

    Requirements Report
    Knowledge Retrieval Results

Содержит:
- Понятые требования
- Непонятные моменты
- Противоречия
- Недостающая информация
- Похожие проекты из памяти
- Похожие решения из памяти

### Artifact Created

    tasks/{task_id}/requirements/requirements_report.md
    tasks/{task_id}/requirements/knowledge_retrieval.md

### Quality Gate
- Все требования проанализированы
- Пробелы идентифицированы
- Память проекта проверена
- Отчёт сформирован

### Agent Role
Requirements Analyzer, Knowledge Retriever

### Documentation Update
- Task history обновлена
- ENGINEERING_HISTORY.md обновлена (если есть важные инсайты)

### Failure Outcome
- Если требования невозможно проанализировать → Task → FAILED

---

## Stage 2: Clarification

### Input
- Requirements Report (из Stage 1)
- Knowledge Retrieval Results (из Stage 1)
- Список пробелов

### Process
Если пробелы есть, агент **не пишет код**.

Он задаёт вопросы:

    Вы хотите поддержку iOS?
    Нужна авторизация?
    Работа офлайн?
    Какие версии Android?
    Какая БД?
    Есть дизайн?

И только после получения ответов переходит дальше.

**Это один из важнейших этапов всей системы.**

> Плохое ТЗ нельзя исправить хорошим кодом.

### Output

    Clarified Requirements

### Artifact Created

    tasks/{task_id}/requirements/clarified_requirements.md

### Quality Gate
- Все пробелы устранены
- Пользователь ответил на все вопросы
- Требования непротиворечивы

### Agent Role
Question Generator

### Documentation Update
- Task status обновлён (если был WAITING)
- Task history обновлена

### Failure Outcome
- Если пользователь не отвечает (таймаут > 7 дней) → Task → FAILED
- Если требования остаются противоречивыми → Task → FAILED

---

## Stage 3: Technical Specification + Constraints + Acceptance Criteria

### Input
- Clarified Requirements (из Stage 2)

### Process
После уточнений агент формирует **внутреннее ТЗ**.

Не пользовательское.
А инженерное.

И выделяет **ограничения** (constraints):

    Flutter
    без Firebase
    SQLite
    Android 9+
    без платных SDK
    работа офлайн
    до 100 Мб

И формулирует **критерии приёмки** (acceptance criteria):

    ✓ Авторизация работает
    ✓ Добавление расходов работает
    ✓ Отчёт строится
    ✓ PDF экспортируется

Именно они потом становятся тестами.

### Output

    Engineering Specification
    Constraints
    Acceptance Criteria

Содержит:
- Стек технологий
- Архитектура
- Модули
- Экраны
- API
- Модели данных
- Тесты
- Quality Requirements
- Constraints (ограничения)
- Acceptance Criteria (критерии приёмки)

### Artifact Created

    tasks/{task_id}/planning/engineering_spec.md
    tasks/{task_id}/requirements/constraints.md
    tasks/{task_id}/requirements/acceptance_criteria.md

### Quality Gate
- Спецификация полная
- Нет противоречий
- Все требования покрыты
- Ограничения явно выделены
- Acceptance criteria сформулированы
- Спецификация инженерная, не пользовательская

### Agent Role
Technical Writer

### Documentation Update
- Task history обновлена
- Project memory обновлена (если есть новые технические решения)

### Failure Outcome
- Если спецификация противоречива → Task → FAILED
- Если ограничения несовместимы → Task → FAILED


---

## Stage 4: Architecture + Decision Records

### Input
- Engineering Specification (из Stage 3)
- Constraints (из Stage 3)
- Architectural Requirements (из Stage 3)

### Process
Только теперь появляется Architect (Architect Agent).

**Важное различие:**
- Stage 3 определил архитектурные требования (что должно быть)
- Stage 4 определяет архитектурные решения (как это будет реализовано)

Architect принимает конкретные решения:

    Riverpod или BLoC?
    Clean Architecture или MVC?
    SQLite или Hive?
    Repository pattern?
    Navigation strategy?

Каждое решение оформляется как **Decision Record** (ADR — Architecture Decision Record):

    ### Decision: State Management

    **Context:**
    Нужно выбрать state management для Flutter-приложения.

    **Alternatives:**
    - Riverpod
    - BLoC
    - Provider

    **Chosen:** Riverpod

    **Reason:**
    - Более современный подход
    - Лучшая тестируемость
    - Меньше boilerplate

    **Consequences:**
    - Команда должна изучить Riverpod
    - Нужно настроить dependency injection

**Важно:** Decision Records могут создаваться на любом Stage, не только на Stage 4.

### Output

    Architectural Decisions
    Decision Records

### Artifact Created

    tasks/{task_id}/planning/architecture_decisions.md
    tasks/{task_id}/planning/decision_records/
      DR-001-state-management.md
      DR-002-database.md

### Quality Gate
- Все архитектурные решения приняты
- Решения обоснованы
- Решения соответствуют спецификации и ограничениям
- Decision Records оформлены

### Agent Role
Architect

### Documentation Update
- Task history обновлена
- ARCHITECTURE.md обновлена (если это новый проект)
- Decision records сохранены

### Failure Outcome
- Если архитектурные решения противоречат ограничениям → Task → FAILED
- Если невозможно выбрать между альтернативами → Task → FAILED

---

## Stage 5: Project Planning + Implementation Plan

### Input
- Engineering Specification (из Stage 3)
- Architectural Decisions (из Stage 4)

### Process
Planner (Planner Agent) строит **не код**, а **дерево проекта**:

    lib/
      presentation/
        screens/
        widgets/
      domain/
        entities/
        usecases/
      data/
        models/
        repositories/
      services/
    tests/
      unit/
      integration/

И определяет, какие файлы будут создаваться.

**И самое важное:** Planner определяет **порядок создания файлов**:

    1. Entity (domain/entities/expense.dart)
    2. Repository Interface (domain/repositories/expense_repository.dart)
    3. Repository Impl (data/repositories/expense_repository_impl.dart)
    4. UseCase (domain/usecases/add_expense.dart)
    5. Provider (presentation/providers/expense_provider.dart)
    6. Screen (presentation/screens/home_screen.dart)

Иначе Coder начнёт писать экран раньше Entity.

### Output

    Project Structure
    File Manifest
    Implementation Plan

### Artifact Created

    tasks/{task_id}/planning/project_manifest.json
    tasks/{task_id}/planning/implementation_plan.json

**project_manifest.json:**

    {
      "files": [
        {"path": "lib/main.dart", "type": "entry_point"},
        {"path": "lib/presentation/screens/home_screen.dart", "type": "ui"},
        {"path": "lib/domain/entities/expense.dart", "type": "model"},
        {"path": "test/unit/expense_test.dart", "type": "test"}
      ]
    }

**implementation_plan.json:**

    {
      "execution_order": [
        {"step": 1, "file": "lib/domain/entities/expense.dart", "depends_on": []},
        {"step": 2, "file": "lib/domain/repositories/expense_repository.dart", "depends_on": ["lib/domain/entities/expense.dart"]},
        {"step": 3, "file": "lib/data/repositories/expense_repository_impl.dart", "depends_on": ["lib/domain/repositories/expense_repository.dart"]},
        {"step": 4, "file": "lib/domain/usecases/add_expense.dart", "depends_on": ["lib/domain/repositories/expense_repository.dart"]},
        {"step": 5, "file": "lib/presentation/providers/expense_provider.dart", "depends_on": ["lib/domain/usecases/add_expense.dart"]},
        {"step": 6, "file": "lib/presentation/screens/home_screen.dart", "depends_on": ["lib/presentation/providers/expense_provider.dart"]}
      ]
    }

### Quality Gate
- Структура проекта определена
- Все файлы перечислены
- Структура соответствует архитектуре
- Порядок создания файлов определён
- Dependencies между файлами учтены

### Agent Role
Project Planner

### Documentation Update
- Task history обновлена
- Project structure задокументирована
- Implementation plan сохранён

### Failure Outcome
- Если структура не соответствует архитектуре → Task → FAILED
- Если dependencies образуют цикл → Task → FAILED

---

## Stage 6: Capability Resolution

### Input
- Implementation Plan (из Stage 5)

### Process
И только теперь начинается поиск возможностей (через Registry Service и другие сервисы).

Потому что уже известно, **что именно строится** и **в каком порядке**.

Агент определяет, какие возможности нужны для каждого файла:

**Capability Map включает:**
- **Skill Map** — навыки (как решать)
- **Tool Map** — инструменты (чем выполнять)
- **Model Selection** — модели LLM для каждой задачи
- **MCP/External Services** — внешние сервисы и API
- **Policies** — политики безопасности и качества
- **Templates** — шаблоны кода и конфигурации

### Output

    Capability Map
    (включает Skill Map, Tool Map, Model Selection, MCP Services, Policies, Templates)

### Artifact Created

    tasks/{task_id}/planning/capability_map.json

Содержит:

    {
      "skills": [
        {"file": "lib/main.dart", "skill": "flutter_entry_point", "priority": "HIGH"},
        {"file": "lib/presentation/screens/home_screen.dart", "skill": "flutter_ui", "priority": "MEDIUM"}
      ],
      "tools": [
        {"file": "lib/main.dart", "tool": "flutter", "action": "build"},
        {"file": "test/unit/expense_test.dart", "tool": "flutter", "action": "test"}
      ],
      "models": [
        {"task": "code_generation", "model": "qwen-2.5-coder-32b"},
        {"task": "review", "model": "qwen-2.5-coder-32b"}
      ],
      "mcp_services": [
        {"name": "database_service", "endpoint": "http://localhost:8080"}
      ],
      "policies": [
        {"type": "security", "rule": "no_hardcoded_secrets"},
        {"type": "quality", "rule": "test_coverage_min_80"}
      ],
      "templates": [
        {"type": "screen", "template": "flutter_screen_template.dart"}
      ]
    }

### Quality Gate
- Все файлы покрыты возможностями
- Навыки доступны в системе
- Инструменты доступны
- Модели выбраны
- Внешние сервисы настроены
- Политики определены
- Шаблоны доступны
- Fallback определён

### Agent Role
Capability Resolver

### Documentation Update
- Task history обновлена
- Capability usage задокументирована

### Failure Outcome
- Если необходимые навыки недоступны → Task → FAILED
- Если инструменты не настроены → Task → FAILED
- Если внешние сервисы недоступны → Task → FAILED


---

## Stage 7: Development

### Input
- Implementation Plan (из Stage 5)
- Capability Map (из Stage 6)

### Process
Вот здесь начинает работать Coder Agent.

Процесс разработки для каждого файла:

    Coder
      ↓
    Review
      ↓
    Compile
      ↓
    Tests
      ↓
    Quality
      ↓
    Fix (если нужно)

Пока файл не станет PASS.

**Важно:** Decision Records могут создаваться на этом этапе:
- Coder решил разбить файл
- Reviewer решил заменить библиотеку
- Tester предложил изменить подход

Coder Agent использует возможности из Capability Map через соответствующие сервисы System Boundaries.

### Output

    Working Code (для каждого файла)
    Decision Records (если были приняты)

### Artifact Created

    tasks/{task_id}/generated/
      lib/
      test/
    tasks/{task_id}/planning/decision_records/
      DR-XXX-file-split.md (если было)

### Quality Gate
- Все файлы написаны
- Все файлы прошли Quality Gates
- Все тесты проходят
- Code review пройден
- Acceptance criteria выполнены

### Agent Role
Coder, Reviewer, Tester, Quality Checker

### Documentation Update
- Task history обновлена
- Code statistics задокументированы
- Decision records сохранены (если были)

### Failure Outcome
- Если тесты не проходят после N итераций → Task → FAILED
- Если code quality ниже порога → Task → FAILED

---

## Stage 8: Integration

### Input
- Working Code (из Stage 7)

### Process
Когда все файлы готовы, Integrator Agent проверяет **проект целиком**.

Именно здесь находятся:
- Architecture Validator
- Dependency Validator
- Circular Dependency checker
- Dead Code detector
- Integration tests

### Output

    Integrated Project
    Integration Report

### Artifact Created

    tasks/{task_id}/reports/integration_report.md

### Quality Gate
- Нет circular dependencies
- Нет dead code
- Все integration tests проходят
- Архитектура не нарушена

### Agent Role
Integration Validator

### Documentation Update
- Task history обновлена
- Integration results задокументированы

### Failure Outcome
- Если circular dependencies найдены → Task → FAILED
- Если integration tests не проходят → Task → FAILED

---

## Stage 9: Engineering Review

### Input
- Integrated Project (из Stage 8)
- Integration Report (из Stage 8)

### Process
Reviewer Agent собирает **пакет изменений** для пользователя:

    ## Summary

    Проект готов к выпуску.

    ## Quality Score

    - Code quality: 95/100
    - Test coverage: 87%
    - Architecture compliance: 100%

    ## Changed Files

    - 15 files created
    - 0 files modified
    - 0 files deleted

    ## Architecture Impact

    - New project structure created
    - Clean Architecture pattern applied
    - Riverpod for state management

    ## Migration Impact

    - No migration needed (new project)

    ## Performance Impact

    - Estimated bundle size: 12MB
    - Expected startup time: <2s

    ## Acceptance Criteria

    ✓ Авторизация работает
    ✓ Добавление расходов работает
    ✓ Отчёт строится
    ✓ PDF экспортируется

### Output

    Review Package

### Artifact Created

    tasks/{task_id}/reports/review_package.md

### Quality Gate
- Пакет полный
- Все метрики собраны
- Информация структурирована
- Acceptance criteria проверены

### Agent Role
Reviewer

### Documentation Update
- Task history обновлена
- Review package сохранён

### Failure Outcome
- Если пакет неполный → Task → FAILED
- Если acceptance criteria не выполнены → Task → FAILED

---

## Stage 10: User Approval

### Input
- Review Package (из Stage 9)

### Process
Вот здесь **заканчиваются полномочия агента**.

Не раньше.

Агент говорит:

    Проект готов.
    Вот изменения.
    Вот Quality Score.
    Вот список решений.
    Подтвердите.

**Важно:** Это точка, где агент останавливается и ждёт подтверждения пользователя (принцип Human Approval).

### Output

    Approved Changes

### Artifact Created

    tasks/{task_id}/reports/approval_record.md

### Quality Gate
- Пользователь подтвердил
- Все вопросы решены
- Финальная версия согласована

### Agent Role
Presenter

### Documentation Update
- Task status → COMPLETED
- Task history обновлена
- Approval record сохранён

### Failure Outcome
- Если пользователь не отвечает (таймаут > 7 дней) → Task → FAILED
- Если пользователь отклоняет → Task → FAILED (или возврат к Stage 9)


---

## Stage 11: Release / Delivery (Optional)

### Input
- Approved Changes (из Stage 10)

### Process
**Этот этап опционален.** Не каждая задача требует релиза.

Агент определяет, требуется ли релиз, на основе типа задачи:
- Продукт → требует релиза
- Библиотека → требует релиза
- Прототип → не требует релиза
- Архитектурный документ → не требует релиза
- Исследование → не требует релиза

Если релиз требуется, агент выполняет:

    commit
      ↓
    push
      ↓
    release / delivery
      ↓
    documentation update
      ↓
    engineering history entry

### Output

    Released Product / Delivered Artifact
    Release Notes
    Updated Documentation
    Engineering History Entry

### Artifact Created

    tasks/{task_id}/reports/release_notes.md
    tasks/{task_id}/artifacts/engineering_history_entry.md

### Quality Gate
- Код закоммичен
- Код запушен
- Релиз создан (если требуется)
- Документация обновлена
- Engineering history записана

### Agent Role
Release Manager, Documentation Writer

### Documentation Update
- RELEASE_NOTES.md обновлена (если был релиз)
- ENGINEERING_HISTORY.md обновлена
- CURRENT_CONTEXT.md обновлён
- Project memory обновлена

### Failure Outcome
- Если commit/push не удался → Task → FAILED
- Если релиз не может быть создан → Task → FAILED

---

## Stage 12: Learning Consolidation

### Input
- Released Product / Delivered Artifact (из Stage 11)
- Все артефакты задачи
- Все decision records
- Все capability candidates (предложенные на предыдущих этапах)

### Process
Именно здесь происходит **консолидация** знаний.

**Важно:** Learning не начинается только на Stage 12.

Learning идёт постоянно:
- Stage 1: Knowledge Retrieval (поиск похожих проектов)
- Stage 7: предложение capability candidates за хорошие паттерны
- Stage 12: консолидация всех знаний

Stage 12 — это **финальная консолидация**, где:
- Все capability candidates получают статус `approved` или `rejected`
- Все lessons learned записываются
- Все метрики собираются
- Все benchmarks обновляются

Процесс консолидации:

    Engineering History
      ↓
    Capability Candidates → Approved Capabilities
      ↓
    Metrics
      ↓
    Benchmark
      ↓
    Lessons Learned
      ↓
    Quality Statistics

### Output

    Lessons Learned
    Approved Capabilities
    Quality Metrics

### Artifact Created

    tasks/{task_id}/reports/lessons_learned.md
    tasks/{task_id}/artifacts/capability_candidates.json (со статусами approved/rejected)
    tasks/{task_id}/artifacts/quality_metrics.json

### Quality Gate
- Lessons learned записаны
- Capability candidates обработаны (approved/rejected)
- Metrics собраны
- Knowledge base обновлена

### Agent Role
Learning Analyst

### Documentation Update
- ENGINEERING_HISTORY.md обновлена
- SKILL_REGISTRY.md обновлена (если есть новые approved skills)
- QUALITY_METRICS.md обновлена
- Project memory обновлена

### Failure Outcome
- Если консолидация не удалась → Task → FAILED (но основные артефакты сохранены)

---

## Quality Gates Summary

Каждый этап имеет чёткий критерий завершения:

| Stage | Quality Gate |
|-------|--------------|
| 0 | Материал принят и распознан |
| 1 | Все требования проанализированы, пробелы идентифицированы, память проверена |
| 2 | Все пробелы устранены, требования непротиворечивы |
| 3 | Спецификация полная, ограничения выделены, acceptance criteria сформулированы |
| 4 | Все архитектурные решения приняты и обоснованы, decision records оформлены |
| 5 | Структура проекта определена, все файлы перечислены, порядок создания определён |
| 6 | Все файлы покрыты возможностями, fallback определён |
| 7 | Все файлы написаны, все тесты проходят, acceptance criteria выполнены |
| 8 | Нет circular dependencies, все integration tests проходят |
| 9 | Пакет изменений полный, все метрики собраны, acceptance criteria проверены |
| 10 | Пользователь подтвердил |
| 11 | Код закоммичен, запушен, релиз создан (если требуется), документация обновлена |
| 12 | Lessons learned записаны, capability candidates обработаны, metrics собраны |


---

## Failure Paths

Не все задачи завершаются успешно. Система должна обрабатывать неудачи.

**Важно:** Failure — это не отдельное состояние, а терминальный исход любого Stage (принцип Failure is Terminal Outcome).

### Failure Scenarios

#### Requirements Impossible

**Симптомы:**
- Требования противоречивы
- Требования нереалистичны
- Пользователь не может ответить на вопросы

**Действия:**
1. Агент документирует проблему
2. Агент предлагает альтернативы
3. Если проблема не решена → Task → FAILED
4. Запись в ENGINEERING_HISTORY.md

#### Architecture Conflict

**Симптомы:**
- Архитектурные решения противоречат друг другу
- Невозможно удовлетворить все требования и ограничения

**Действия:**
1. Агент выявляет конфликт
2. Агент предлагает компромиссы
3. Если конфликт не решён → Task → FAILED
4. Запись в ENGINEERING_HISTORY.md

#### Tests Never Pass

**Симптомы:**
- Тесты не проходят после N итераций
- Code quality ниже порога

**Действия:**
1. Агент анализирует причину
2. Агент предлагает упрощение
3. Если проблема не решена → Task → FAILED
4. Запись в ENGINEERING_HISTORY.md

#### User Disappeared

**Симптомы:**
- Пользователь не отвечает на вопросы (Stage 2)
- Пользователь не подтверждает (Stage 10)
- Таймаут > 7 дней

**Действия:**
1. Агент отправляет напоминание
2. Если нет ответа → Task → FAILED
3. Запись в ENGINEERING_HISTORY.md

#### Build Impossible

**Симптомы:**
- Невозможно собрать проект
- Зависимости несовместимы
- Окружение не настроено

**Действия:**
1. Агент анализирует причину
2. Агент предлагает решения
3. Если проблема не решена → Task → FAILED
4. Запись в ENGINEERING_HISTORY.md

### Failure Documentation

Каждая неудача должна быть задокументирована:
- Что пошло не так?
- Почему это произошло?
- Что можно улучшить?
- Как предотвратить в будущем?

---

## Documentation Updates

После завершения каждого Stage агент обязан обновить проектную документацию.

### Documentation Update Questions

После каждого Stage агент должен ответить на 5 вопросов:

1. **Что изменилось?** — какие артефакты появились, какие файлы созданы
2. **Что нужно сохранить?** — какие знания важны для будущих задач
3. **Какие документы требуют обновления?** — какие документы в memory-репозитории нужно обновить
4. **Какие новые знания появились?** — что агент узнал нового
5. **Можно ли использовать их повторно?** — есть ли паттерны, которые можно извлечь

### Documentation Update Matrix

| Stage | Documentation Updated |
|-------|----------------------|
| 0 | Task created, Workspace created, CURRENT_CONTEXT.md |
| 1 | Task history, ENGINEERING_HISTORY.md (если есть инсайты), Knowledge Retrieval results |
| 2 | Task status, Task history |
| 3 | Task history, Project memory, Constraints, Acceptance Criteria |
| 4 | Task history, ARCHITECTURE.md, Decision records |
| 5 | Task history, Project structure, Implementation plan |
| 6 | Task history, Capability usage |
| 7 | Task history, Code statistics, Decision records (если были) |
| 8 | Task history, Integration results |
| 9 | Task history, Review package |
| 10 | Task status → APPROVED, Task history, Approval record |
| 11 | Task status → DELIVERED, RELEASE_NOTES.md (если был релиз), ENGINEERING_HISTORY.md, CURRENT_CONTEXT.md, Project memory |
| 12 | Task status → COMPLETED, ENGINEERING_HISTORY.md, CAPABILITY_REGISTRY.md (если есть новые approved capabilities), QUALITY_METRICS.md, Project memory |

### Documentation Principle

> Документация не является пассивным архивом.
> Она является частью жизненного цикла задачи.

---

## Stage Transitions

Переходы между этапами:

    Stage 0 → Stage 1: Raw Requirements ready
    Stage 1 → Stage 2: Requirements Report ready
    Stage 2 → Stage 3: Clarified Requirements ready (или цикл вопросов)
    Stage 3 → Stage 4: Engineering Specification ready
    Stage 4 → Stage 5: Architectural Decisions ready
    Stage 5 → Stage 6: Implementation Plan ready
    Stage 6 → Stage 7: Capability Map ready
    Stage 7 → Stage 8: All files PASS
    Stage 8 → Stage 9: Integration Report ready
    Stage 9 → Stage 10: Review Package ready
    Stage 10 → Stage 11: User approved (или переход к Stage 12, если релиз не требуется)
    Stage 11 → Stage 12: Release/Delivery complete (или переход к Stage 12, если Stage 11 пропущен)
    Stage 12 → End: Learning consolidation complete

### Обратные переходы

Некоторые этапы могут возвращаться назад:
- Stage 2 → Stage 1: если обнаружены новые пробелы
- Stage 7 → Stage 7: цикл Coder → Review → Fix до PASS
- Stage 8 → Stage 7: если integration tests не проходят
- Stage 10 → Stage 9: если пользователь запросил изменения

### Failure transitions

При неудаче:
- Любой Stage → FAILED: если проблема не может быть решена

---

## End of Document

Этот документ определяет полный жизненный цикл пользовательской задачи в системе Agent Developer.

Он является контрактом между бизнес-задачей и всеми техническими компонентами системы.

Все будущие runtime-компоненты (LangGraph, FSM, Tools, Memory) будут реализовывать этот процесс.

Это первое архитектурное решение, которое отличает Agent Developer от "очередного LangGraph-проекта".

### Ключевые принципы

1. **Task is Primary Object** — задача, а не файл, является первичным объектом
2. **Documentation First** — документация обновляется после каждого этапа
3. **Human Approval** — финальное решение за пользователем
4. **Continuous Learning** — система учится на каждом завершённом проекте
5. **Code is Middle** — код находится в середине процесса, а не является его центром
6. **Failure is Terminal Outcome** — неудача это терминальный исход любого Stage
7. **Release is Optional** — не каждая задача требует релиза

> Разработчик не начинает с кода. Он начинает с понимания задачи.

Все технические компоненты должны служить этому процессу, а не наоборот.

