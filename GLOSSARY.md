# Glossary (Глоссарий)

**Status:** ACCEPTED
**Version:** 2.0
**Date:** 2026-07-10
**Authority:** Project Architect
**Maintainer:** Documentation Maintainer

**Type:** Registry (Layer 3: Engineering Knowledge)
**Primary Question:** "What engineering terminology is used in this project?"
**Canonical Source for:** Engineering terminology registry
**Dependencies:** INFORMATION_ARCHITECTURE.md, DOC_STANDARD.md, PROGRAM_MANAGEMENT.md, DOMAIN_ARCHITECTURE.md
**Dependents:** All engineering documents

---

## Purpose (Назначение)

Этот документ предоставляет единый реестр инженерной терминологии проекта Agent Developer.

Каждая запись включает краткое определение, категорию и ссылку на канонический документ.

---

## Scope (Область применения)

Этот документ определяет реестр инженерной терминологии и правила его использования.

Он не определяет инженерную семантику зарегистрированных терминов. Инженерная семантика находится в соответствующих Canonical Source.

**Category** предоставляется только для навигации и не определяет инженерную семантику. Categories are organizational only.

**Definition** предоставляет только краткое идентифицирующее описание. Полные определения находятся в Canonical Source.

Если определение в этом реестре отличается от его Canonical Source, Canonical Source всегда имеет приоритет.

---

## Categories (Категории)

The following Category values are defined by this registry:

- Core Engineering
- Information Architecture
- Lifecycle Categories
- Document Types
- Document Status
- Program Concepts
- Program Lifecycle States
- Engineering Process
- Release Management
- Automation
- Runtime Concepts
- Runtime Components
- Engineering History

---

## Availability (Доступность)

Availability may be specified only when the Canonical Source is not yet available.

Allowed values:

- Planned

---

## Ordering (Порядок)

Terms inside each category shall be ordered alphabetically by English term unless another order is explicitly required.

---

## Core Engineering (Базовые инженерные понятия)

### ADR (Architecture Decision Record)

**Category:** Core Engineering

**Definition:** Запись об архитектурном решении с контекстом, обоснованием и последствиями.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Artifact (Артефакт)

**Category:** Core Engineering

**Definition:** Версионируемый инженерный результат.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Authority (Authority)

**Category:** Core Engineering

**Definition:** Роль, определяющая содержимое и структуру документа.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Canonical Source (Канонический источник)

**Category:** Core Engineering

**Definition:** Единственное авторитетное место хранения инженерного факта.

**Canonical Source:** DOC_STANDARD.md

### Dependencies (Зависимости)

**Category:** Core Engineering

**Definition:** Документы, которые читает данный документ.

**Canonical Source:** DOC_STANDARD.md

### Dependents (Зависимые документы)

**Category:** Core Engineering

**Definition:** Документы, которые читают данный документ.

**Canonical Source:** DOC_STANDARD.md

### Engineering Invariant (Инженерный инвариант)

**Category:** Core Engineering

**Definition:** Фундаментальное правило, которое должно всегда соблюдаться в своей области применения.

**Canonical Source:** DOC_STANDARD.md

### Evidence (Evidence)

**Category:** Core Engineering

**Definition:** Неизменяемый артефакт, подтверждающий состояние или поведение проекта.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Knowledge Item (Единица знания)

**Category:** Core Engineering

**Definition:** Фрагмент инженерного знания, зафиксированный в документации.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Lifecycle (Жизненный цикл)

**Category:** Core Engineering

**Definition:** Последовательность состояний, через которые проходит артефакт.

**Canonical Source:** DOC_STANDARD.md

### Maintainer (Maintainer)

**Category:** Core Engineering

**Definition:** Роль, выполняющая обновления и исправления документа.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Primary Question (Основной вопрос)

**Category:** Core Engineering

**Definition:** Фундаментальный вопрос, на который отвечает документ.

**Canonical Source:** DOC_STANDARD.md

### Release (Релиз)

**Category:** Core Engineering

**Definition:** Версионированный снимок проекта, передаваемый пользователям.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Source of Truth (Источник истины)

**Category:** Core Engineering

**Definition:** Документ или система, из которой берутся достоверные факты.

**Canonical Source:** PROJECT_PROTOCOL.md

### Task (Задача)

**Category:** Core Engineering

**Definition:** Доменная сущность, представляющая единицу инженерной работы.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Validation (Валидация)

**Category:** Core Engineering

**Definition:** Процесс проверки доказательств на соответствие критериям приёмки.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Workspace (Рабочее пространство)

**Category:** Core Engineering

**Definition:** Среда, в которой выполняются инженерные активности.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

---

## Information Architecture (Информационная архитектура)

### Engineering Knowledge (Инженерные знания)

**Category:** Information Architecture

**Definition:** Layer 3 — определяет, как проект разрабатывается и поддерживается.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Layer (Слой)

**Category:** Information Architecture

**Definition:** Уровень организации знаний в информационной архитектуре.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Meta Architecture (Мета-архитектура)

**Category:** Information Architecture

**Definition:** Layer 0 — описывает саму систему знаний.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Operational Knowledge (Операционные знания)

**Category:** Information Architecture

**Definition:** Layer 2 — описывает текущее операционное состояние проекта.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Project Identity (Идентичность проекта)

**Category:** Information Architecture

**Definition:** Layer 1 — определяет идентичность проекта, роли, принципы.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Verification Layer (Слой верификации)

**Category:** Information Architecture

**Definition:** Layer 4 — содержит неизменяемые артефакты-доказательства.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

---

## Lifecycle Categories (Категории жизненного цикла)

### Dynamic (Динамический)

**Category:** Lifecycle Categories

**Definition:** Жизненный цикл для документов, меняющихся постоянно.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Immutable (Неизменяемый)

**Category:** Lifecycle Categories

**Definition:** Жизненный цикл для артефактов, создаваемых один раз без изменений.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Semi-static (Полустатический)

**Category:** Lifecycle Categories

**Definition:** Жизненный цикл для документов, меняющихся периодически.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Static (Статический)

**Category:** Lifecycle Categories

**Definition:** Жизненный цикл для документов, которые почти никогда не меняются.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

---

## Document Types (Типы документов)

### Architecture (Архитектура)

**Category:** Document Types

**Definition:** Тип документа, определяющий структуру системы.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Context (Контекст)

**Category:** Document Types

**Definition:** Тип документа, описывающий текущее состояние проекта.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### History (История)

**Category:** Document Types

**Definition:** Тип документа, записывающий прошлые события.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Index (Индекс)

**Category:** Document Types

**Definition:** Тип документа, помогающий находить информацию (навигация).

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Playbook (Руководство)

**Category:** Document Types

**Definition:** Тип документа, определяющий последовательность действий.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Protocol (Протокол)

**Category:** Document Types

**Definition:** Тип документа, определяющий правила взаимодействия и ответственности.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Registry (Реестр)

**Category:** Document Types

**Definition:** Тип документа, определяющий авторитетный инвентарь сущностей проекта.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

### Standard (Стандарт)

**Category:** Document Types

**Definition:** Тип документа, определяющий требования к артефактам.

**Canonical Source:** INFORMATION_ARCHITECTURE.md

---

## Document Status (Статусы документов)

### ACCEPTED (Принят)

**Category:** Document Status

**Definition:** Статус утверждённого документа или решения.

**Canonical Source:** DOCUMENTS.md

### ACTIVE (Активен)

**Category:** Document Status

**Definition:** Статус действующего документа.

**Canonical Source:** DOCUMENTS.md

### ARCHIVED (Архивирован)

**Category:** Document Status

**Definition:** Статус документа, сохранённого для исторической справки.

**Canonical Source:** DOCUMENTS.md

### DEPRECATED (Устарел)

**Category:** Document Status

**Definition:** Статус документа, который больше не рекомендуется к использованию.

**Canonical Source:** DOCUMENTS.md

### PLANNED (Запланирован)

**Category:** Document Status

**Definition:** Статус документа, который планируется создать.

**Canonical Source:** DOCUMENTS.md

### PROPOSED (Предложен)

**Category:** Document Status

**Definition:** Статус документа или решения, ожидающего утверждения.

**Canonical Source:** DOCUMENTS.md

### SUPERSEDED (Заменён)

**Category:** Document Status

**Definition:** Статус документа, заменённого новой версией.

**Canonical Source:** DOCUMENTS.md

---

## Program Concepts (Понятия управления программами)

### Architecture Review (Архитектурное рецензирование)

**Category:** Program Concepts

**Definition:** Формальная оценка плана программы до его заморозки.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Backlog (Бэклог)

**Category:** Program Concepts

**Definition:** Очередь идей и будущих работ.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Frozen Plan (Замороженный план)

**Category:** Program Concepts

**Definition:** Утверждённый план, который не может быть изменён в процессе исполнения.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Milestone (Контрольная точка)

**Category:** Program Concepts

**Definition:** Значимый контрольный этап внутри программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Phase (Фаза)

**Category:** Program Concepts

**Definition:** Отдельный этап жизненного цикла программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Program (Программа)

**Category:** Program Concepts

**Definition:** Инженерная инициатива с ограниченными границами, выполняемая в соответствии с Frozen Plan.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Program Evaluation (Оценка программы)

**Category:** Program Concepts

**Definition:** Процесс оценки программы (Review + Retrospective).

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Program Plan (План программы)

**Category:** Program Concepts

**Definition:** Замороженный план конкретной программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Retrospective (Ретроспектива)

**Category:** Program Concepts

**Definition:** Структурированный анализ после завершения программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Review (Рецензирование)

**Category:** Program Concepts

**Definition:** Формальная точка оценки программы. В зависимости от контекста термин также может обозначать одноимённое состояние жизненного цикла программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Single Active Program (Единственная активная программа)

**Category:** Program Concepts

**Definition:** Инвариант: одновременно активна только одна программа.

**Canonical Source:** PROGRAM_MANAGEMENT.md

---

## Program Lifecycle States (Состояния жизненного цикла программ)

### Archived (Архивирована)

**Category:** Program Lifecycle States

**Definition:** Состояние программы, сохранённой для исторической справки.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Completed (Завершена)

**Category:** Program Lifecycle States

**Definition:** Состояние успешно завершённой программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Draft (Черновик)

**Category:** Program Lifecycle States

**Definition:** Начальное состояние программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### Frozen (Заморожена)

**Category:** Program Lifecycle States

**Definition:** Состояние программы после утверждения плана.

**Canonical Source:** PROGRAM_MANAGEMENT.md

### In Progress (Выполняется)

**Category:** Program Lifecycle States

**Definition:** Состояние активной исполняемой программы.

**Canonical Source:** PROGRAM_MANAGEMENT.md

---

## Engineering Process (Инженерные процессы)

### Change Management (Управление изменениями)

**Category:** Engineering Process

**Definition:** Процесс управления изменениями в проекте.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Development Workflow (Рабочий процесс разработки)

**Category:** Engineering Process

**Definition:** Последовательность фаз разработки.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Documentation First (Документация прежде всего)

**Category:** Engineering Process

**Definition:** Практика документирования до реализации.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Red-Green-Refactor (Red-Green-Refactor)

**Category:** Engineering Process

**Definition:** Цикл TDD: failing test → passing test → refactor.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Smoke Testing (Дымовое тестирование)

**Category:** Engineering Process

**Definition:** Быстрая проверка работоспособности после изменений.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### TDD (Test-Driven Development)

**Category:** Engineering Process

**Definition:** Разработка через тестирование.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Verification Pipeline (Конвейер верификации)

**Category:** Engineering Process

**Definition:** Стандартизированный процесс верификации артефактов.

**Canonical Source:** ENGINEERING_PLAYBOOK.md

### Vertical Slice (Вертикальный срез)

**Category:** Engineering Process

**Definition:** Вертикальный срез функциональности для end-to-end тестирования.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

---

## Release Management (Управление релизами)

### Baseline (Baseline)

**Category:** Release Management

**Definition:** Зафиксированная стабильная версия для сравнения.

**Canonical Source:** REPOSITORIES.md

### Hotfix Release (Hotfix релиз)

**Category:** Release Management

**Definition:** Экстренный релиз для критических исправлений.

**Canonical Source:** RELEASE_PROCESS.md

### Major Release (Major релиз)

**Category:** Release Management

**Definition:** Релиз с обратно-несовместимыми изменениями API.

**Canonical Source:** RELEASE_PROCESS.md

### Minor Release (Minor релиз)

**Category:** Release Management

**Definition:** Релиз с новыми функциональностями, совместимый с предыдущими.

**Canonical Source:** RELEASE_PROCESS.md

### Patch Release (Patch релиз)

**Category:** Release Management

**Definition:** Релиз с исправлениями ошибок, полностью совместимый.

**Canonical Source:** RELEASE_PROCESS.md

### Semantic Versioning (Семантическое версионирование)

**Category:** Release Management

**Definition:** Схема версионирования SemVer с компонентами MAJOR.MINOR.PATCH.

**Canonical Source:** RELEASE_PROCESS.md

### SemVer MAJOR (SemVer MAJOR)

**Category:** Release Management

**Definition:** Первая часть SemVer, увеличивается при breaking changes.

**Canonical Source:** RELEASE_PROCESS.md

### SemVer MINOR (SemVer MINOR)

**Category:** Release Management

**Definition:** Вторая часть SemVer, увеличивается при новых функциях.

**Canonical Source:** RELEASE_PROCESS.md

### SemVer PATCH (SemVer PATCH)

**Category:** Release Management

**Definition:** Третья часть SemVer, увеличивается при исправлениях.

**Canonical Source:** RELEASE_PROCESS.md

---

## Automation (Автоматизация)

### Automation Registry (Реестр автоматизации)

**Category:** Automation

**Definition:** Авторитетный список автоматизированных проверок проекта.

**Canonical Source:** AUTOMATION.md

### Continuous Integration (CI)

**Category:** Automation

**Definition:** Практика непрерывной интеграции изменений в проект.

**Canonical Source:** AUTOMATION.md

### Idempotent (Идемпотентный)

**Category:** Automation

**Definition:** Свойство операции давать одинаковый результат при многократном выполнении.

**Canonical Source:** AUTOMATION.md

### Manual Verification (Ручная верификация)

**Category:** Automation

**Definition:** Проверка, выполняемая инженером.

**Canonical Source:** AUTOMATION.md

### Pre-commit Verification (Pre-commit верификация)

**Category:** Automation

**Definition:** Проверка, выполняемая перед commit.

**Canonical Source:** AUTOMATION.md

### Pre-push Verification (Pre-push верификация)

**Category:** Automation

**Definition:** Проверка, выполняемая перед push в remote.

**Canonical Source:** AUTOMATION.md

### Trigger Model (Модель триггеров)

**Category:** Automation

**Definition:** Модель триггеров автоматизации (pre-commit, pre-push, CI).

**Canonical Source:** AUTOMATION.md

---

## Runtime Concepts (Концепции Runtime)

### Agent Runtime (Agent Runtime)

**Category:** Runtime Concepts

**Definition:** Исполняемая среда агента.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Five-Level Architecture (Пятиуровневая архитектура)

**Category:** Runtime Concepts

**Definition:** Пятиуровневая архитектура Agent Developer Runtime.

**Canonical Source:** RUNTIME_ARCHITECTURE.md

**Availability:** Planned

---

## Runtime Components (Компоненты Runtime)

### Capability Resolver (Capability Resolver)

**Category:** Runtime Components

**Definition:** Компонент разрешения capabilities агента.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Context Manager (Context Manager)

**Category:** Runtime Components

**Definition:** Компонент управления контекстом выполнения.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Event Bus (Шина событий)

**Category:** Runtime Components

**Definition:** Шина событий для межкомпонентного взаимодействия.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Execution Engine (Execution Engine)

**Category:** Runtime Components

**Definition:** Компонент, выполняющий workflow.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Finite State Machine (FSM)

**Category:** Runtime Components

**Definition:** Автомат состояний для управления workflow.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Memory Engine (Memory Engine)

**Category:** Runtime Components

**Definition:** Компонент управления памятью и knowledge items.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Orchestrator (Оркестратор)

**Category:** Runtime Components

**Definition:** Компонент, координирующий выполнение задач агента.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

### Runtime Engine (Runtime Engine)

**Category:** Runtime Components

**Definition:** Ядро исполнения Agent Developer.

**Canonical Source:** DOMAIN_ARCHITECTURE.md

**Availability:** Planned

---

## Engineering History (Инженерная история)

### Impact (Влияние)

**Category:** Engineering History

**Definition:** Описание того, на что повлиял инцидент.

**Canonical Source:** ENGINEERING_HISTORY.md

### Lessons Learned (Извлечённые уроки)

**Category:** Engineering History

**Definition:** Записи об уроках, извлечённых в процессе разработки.

**Canonical Source:** ENGINEERING_HISTORY.md

### Post-mortem (Пост-мортем)

**Category:** Engineering History

**Definition:** Анализ инцидентов и сбоев после их возникновения.

**Canonical Source:** ENGINEERING_HISTORY.md

### Prevention (Предотвращение)

**Category:** Engineering History

**Definition:** Меры предотвращения повторения проблем.

**Canonical Source:** ENGINEERING_HISTORY.md

### Root Cause (Корневая причина)

**Category:** Engineering History

**Definition:** Базовая причина инцидента или проблемы.

**Canonical Source:** ENGINEERING_HISTORY.md

### Severity (Серьёзность)

**Category:** Engineering History

**Definition:** Уровень серьёзности инцидента (Critical/High/Medium/Low).

**Canonical Source:** ENGINEERING_HISTORY.md

---

## Related Documents (Связанные документы)

- INFORMATION_ARCHITECTURE.md
- DOC_STANDARD.md
- PROGRAM_MANAGEMENT.md
- DOMAIN_ARCHITECTURE.md
- RUNTIME_ARCHITECTURE.md

---

## Usage Rules (Правила использования)

1. Все документы должны использовать терминологию, согласованную с настоящим реестром и соответствующими Canonical Source.
2. Если термин отсутствует в данном реестре, используется оригинальное английское написание до его официального добавления.
3. При переводе допускается добавление пояснения на русском при первом упоминании, но английский термин остаётся основным.
4. Изменения в терминологии должны сохранять согласованность с каноническим документом, определяющим соответствующее понятие.
5. New engineering terminology shall be registered in this registry before its first normative use in project documentation.
6. Removing a term from the registry requires review of all dependent documentation.

---

## Engineering Invariant (Инженерный инвариант)

**Engineering Invariant:** Every engineering term used throughout the project shall have exactly one registry entry and exactly one Canonical Source.

---

## Definition of Done (Критерий готовности)

**Definition of Done:** Every engineering term used in project documentation is either registered in this document or intentionally left in its original English form until officially registered.

---

## End of Document (Конец документа)

Этот документ предоставляет единый реестр терминологии для проекта Agent Developer.

Все инженерные документы должны использовать терминологию, зарегистрированную в данном документе и определённую соответствующими Canonical Source.
