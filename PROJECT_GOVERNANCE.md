# Project Governance

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-21  
**Authority:** Project Architect  
**Maintainer:** Project Architect  

**Type:** Constitution + Governance (Layer 0: Meta Strategy)  
**Primary Question:** "По каким правилам развивается система Agent Developer?"  
**Canonical Source for:** Constitution, vision, products, goals, phases, invariants, principles, governance process, change classification, deferred decisions  
**Dependencies:** DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md, TASK_LIFECYCLE.md  
**Dependents:** LAYER3_ROADMAP.md, все будущие планы реализации  
**Lifecycle:** Static (изменяется только при фундаментальных сдвигах)  
**Priority:** **Стратегический** — имеет приоритет в вопросах стратегии, принципов управления и архитектурных законов. Доменные определения принадлежат DOMAIN_ARCHITECTURE, а детали реализации — документам соответствующих слоёв.

---

> **PROJECT_GOVERNANCE объединяет в себе два логических раздела:**
> **Project Constitution (Vision, Supreme Law, Invariants, Principles)**
> **и Governance Model (Process, Change Classification, Decisions, Phases).**
>
> **При росте системы эти разделы могут быть выделены в самостоятельные документы**
> **без изменения их содержания.**

---

## Project Constitution

Этот документ определяет не архитектуру, не реализацию, не план работ,
а правила, по которым изменяются все остальные документы проекта.

### Приоритет документа

PROJECT_GOVERNANCE имеет приоритет в вопросах стратегии, принципов управления и архитектурных законов.

Доменные определения принадлежат DOMAIN_ARCHITECTURE.

Детали реализации принадлежат документам соответствующих слоёв.

Это разделение компетенций предотвращает смешение уровней абстракции.

Этот документ может быть изменён только через Governance Process (см. раздел ниже).

---

## Supreme Law

> **Agent Developer максимально автоматизирует инженерную деятельность,**
> **сохраняя за человеком ответственность за стратегические решения**
> **и изменение архитектурной политики.**

Этот закон объединяет:
- Автоматизацию реализации
- Human Approval
- Approval Gates
- Architectural Impact
- Quality Gates
- Долгосрочную память
- Composite Skills
- Инженерную ответственность

Человек остаётся **Engineering Lead**, а агент постепенно становится
максимально самостоятельным исполнителем инженерной политики.

---

## Vision

**Agent Developer** — это инженерная система, объединяющая память, исполнение,
инструменты и интеллектуальных агентов в единый процесс разработки
программного обеспечения.

**Цель проекта — не заменить инженера, а увеличить объём инженерной работы,**
**который может быть выполнен без потери качества и управляемости.**

*По аналогии с операционной системой, LLM является лишь одним из компонентов
этой инженерной системы.*

### Три независимых продукта

Проект состоит из трёх независимых продуктов:

    agent-developer-memory (Engineering Memory System)
                │
                ▼
    agent-developer-runtime (Исполнитель политики)
                │
                ▼
    Agent Developer (Композиция: Memory + Runtime + LLM + Tools)

Каждый продукт имеет свою ответственность, свой жизненный цикл и свои критерии успеха.


---

## Three Products

### 1. agent-developer-memory

**Что это:** Engineering Memory System

**Не является:**
- Памятью пользователя
- Памятью LLM
- RAG-системой

**Является:**
- Источником истины для архитектуры
- Хранилищем инженерных знаний
- Системой управления решениями
- **Платформой для других инженерных систем**

**Отвечает на вопросы:**
- Почему принято решение?
- Почему отвергнут другой вариант?
- Какие ограничения существуют?
- Какая сейчас стадия проекта?
- Что считается завершением?
- Какие знания уже накоплены?

**Репозиторий:** `agent-developer-memory` (текущий)

### 2. agent-developer-runtime

**Что это:** Исполнитель политики

**Не является:**
- Автор архитектуры
- Приниматель решений

**Является:**
- Читателем памяти проекта
- Исполнителем политики
- Координатором агентов

**Принцип:** Runtime не должен знать, почему архитектура именно такая.
Он должен читать память проекта и выполнять её.

**Репозиторий:** `agent-developer-runtime` (будущий)

### 3. Agent Developer

**Что это:** Композиция

**Состав:**
    Memory + Runtime + LLM + Tools + Skills + Project Memory

**Принцип:** Агент не равен Runtime. Агент — это композиция всех компонентов.

**Репозиторий:** `agent-developer` (будущий, финальный продукт)

---

## Product Definitions

### agent-developer-memory (Engineering Memory System)

**Maturity:** Baseline Complete (Layer 2)

**Mission:**
Memory остаётся единственным источником инженерной памяти для всей системы.
Engineering Memory должна быть пригодна для использования не только Runtime данного проекта,
но и другими инженерными системами.

**Success Criteria:**
- Документация полная и непротиворечивая
- Архитектура независима от реализации
- Все сущности имеют чёткие контракты
- Жизненный цикл задачи определён
- Memory может быть использована другим Runtime без изменений
- Memory может быть использована другой инженерной системой

**Платформенное свойство:**
Memory — это не просто репозиторий документации. Это самостоятельный продукт,
который может служить основой для других инженерных систем.

### agent-developer-runtime (Execution Engine)

**Maturity:** Planned (Layer 3)

**Mission:**
Runtime исполняет Task Lifecycle, читая память проекта и координируя агентов,
не принимая архитектурных решений самостоятельно.

**Success Criteria:**
- Может выполнять Task Lifecycle от Stage 0 до Stage 12
- Агенты могут выполнять свои роли
- Tools могут выполняться
- Knowledge Retrieval работает
- Система устойчива к сбоям

### Agent Developer (Final Product)

**Maturity:** Planned (композиция memory + runtime)

**Mission:**
Автономная разработка программного обеспечения с сохранением
стратегической ответственности за человеком.

**Success Criteria:**
- Может разработать реальное приложение по требованиям
- Может обучаться на выполненных задачах
- Может управлять знаниями
- Может координировать множество агентов


---

## Strategic Goals

### Goal 1: Complete Architecture Foundation

**Цель:** Завершить архитектурный фундамент Layer 2

**Status:** ✅ COMPLETED

**Definition of Done:**
- ✅ PROJECT_PROTOCOL.md создан
- ✅ DOMAIN_ARCHITECTURE.md создан
- ✅ SYSTEM_BOUNDARIES.md создан
- ✅ TASK_LIFECYCLE.md создан
- ✅ Архитектура независима от реализации
- ✅ Все сущности имеют чёткие контракты

### Goal 2: Establish Project Governance

**Цель:** Создать конституцию проекта

**Status:** 🚧 IN PROGRESS

**Definition of Done:**
- ⏳ PROJECT_GOVERNANCE.md создан и утверждён
- ⏳ Supreme Law сформулирован
- ⏳ Governance Process определён
- ⏳ Change Classification определена

### Goal 3: Design Runtime Architecture

**Цель:** Спроектировать архитектуру Runtime (Layer 3)

**Status:** 🚧 PLANNED

**Definition of Done:**
- ⏳ LAYER3_ROADMAP.md создан и утверждён
- ⏳ Архитектура Runtime согласована с Layer 2
- ⏳ Все компоненты определены
- ⏳ Зависимости между компонентами определены

### Goal 4: Implement Minimal Viable Runtime

**Цель:** Реализовать минимальный рабочий Runtime

**Status:** 🚧 PLANNED

**Definition of Done:**
- ⏳ Vertical Slice проходит полностью
- ⏳ Task может проходить через Stage 0-12
- ⏳ FSM доказана интеграционными тестами
- ⏳ Runtime использует Engineering Memory

### Goal 5: Integrate Agents

**Цель:** Интегрировать агентов в Runtime

**Status:** 🚧 PLANNED

**Definition of Done:**
- ⏳ Агенты могут выполнять свои роли
- ⏳ Knowledge Retrieval работает
- ⏳ Tools могут выполняться
- ⏳ Capability Resolution работает
- ⏳ Интеграционные тесты проходят

### Goal 6: Create Final Product

**Цель:** Создать финальный продукт Agent Developer

**Status:** 🚧 FUTURE

**Definition of Done:**
- ⏳ agent-developer-memory интегрирован
- ⏳ agent-developer-runtime интегрирован
- ⏳ LLM интегрирован
- ⏳ Tools интегрированы
- ⏳ Система может разработать реальное приложение

---

## Operating Principles

### Principle 1: Documentation → Implementation → Verification → Knowledge Consolidation → Documentation

**Правило:** Цикл разработки всегда следует этому порядку

**Обоснование:** Документация — это источник истины. Реализация следует за документацией.
Проверка подтверждает реализацию. Консолидация знаний обновляет документацию.

### Principle 2: Decision First

**Правило:** Сначала принимаются решения, потом пишется код

**Обоснование:** Решения должны быть обоснованы и задокументированы до начала реализации.

### Principle 3: Documentation First

**Правило:** Документация всегда предшествует реализации

**Обоснование:** Документация — это источник истины. Реализация следует за документацией,
а не наоборот.

### Principle 4: Human Approval

**Правило:** High Impact решения требуют подтверждения пользователя

**Обоснование:** Соответствует Supreme Law — человек остаётся Engineering Lead.

### Principle 5: Continuous Learning

**Правило:** Система учится на каждом завершённом проекте

**Обоснование:** Knowledge Items создаются непрерывно, а не только в конце.

### Principle 6: Evidence before Optimization

**Правило:** Сначала доказательства, потом оптимизация

**Обоснование:** Оптимизация без доказательств — это преждевременная оптимизация.

### Principle 7: Architecture before Code

**Правило:** Сначала архитектура, потом код

**Обоснование:** Код без архитектуры — это хаос.


---

## Development Phases

### Phase 0: Architecture Foundation

**Status:** ✅ COMPLETED  
**Priority:** Critical

**Цель:** Создать архитектурный фундамент

**Definition of Done:**
- ✅ Все документы Layer 2 созданы
- ✅ Архитектура согласована
- ✅ Документы не противоречат друг другу

**Результат:** Архитектурный фундамент завершён

### Phase 1: Strategic Planning

**Status:** 🚧 IN PROGRESS  
**Priority:** Critical

**Цель:** Создать конституцию проекта и план реализации Runtime

**Definition of Done:**
- ⏳ PROJECT_GOVERNANCE.md создан и утверждён
- ⏳ LAYER3_ROADMAP.md создан и утверждён
- ⏳ Приоритеты определены

**Результат:** Стратегический план готов

### Phase 2: Runtime Foundation

**Status:** 🚧 PLANNED  
**Priority:** Critical

**Цель:** Создать исполняемую платформу, реализующую архитектурную модель

**Definition of Done:**
- ⏳ Runtime способен выполнять Task Lifecycle
- ⏳ Runtime использует Engineering Memory
- ⏳ Runtime поддерживает агентов
- ⏳ Vertical Slice проходит полностью

**Результат:** Минимальный рабочий Runtime

### Phase 3: Agent Integration

**Status:** 🚧 PLANNED  
**Priority:** High

**Цель:** Интегрировать агентов в Runtime

**Definition of Done:**
- ⏳ Агенты могут выполнять свои роли
- ⏳ Knowledge Retrieval работает
- ⏳ Tools могут выполняться
- ⏳ Capability Resolution работает
- ⏳ Интеграционные тесты проходят

**Результат:** Runtime с интегрированными агентами

### Phase 4: Production Ready

**Status:** 🚧 FUTURE  
**Priority:** Medium

**Цель:** Сделать систему надёжной и масштабируемой

**Definition of Done:**
- ⏳ Система устойчива к сбоям
- ⏳ Можно восстанавливать состояние
- ⏳ События доставляются гарантированно
- ⏳ Производительность приемлема
- ⏳ Документация полная

**Результат:** Production-ready Runtime

### Phase 5: Final Product

**Status:** 🚧 FUTURE  
**Priority:** Medium

**Цель:** Создать финальный продукт Agent Developer

**Definition of Done:**
- ⏳ Система может разработать реальное приложение
- ⏳ Система может обучаться на выполненных задачах
- ⏳ Система может управлять знаниями
- ⏳ Система может координировать множество агентов
- ⏳ Пользовательская документация полная

**Результат:** Финальный продукт Agent Developer


---

## Governance Process

### Кто имеет право менять Конституцию?

Только **Project Architect** через процесс, описанный в PROJECT_PROTOCOL.md.

### Когда может быть изменён PROJECT_GOVERNANCE?

PROJECT_GOVERNANCE может быть изменён только если:

- Меняется архитектурная стратегия проекта
- Появляется новый продукт (четвёртый независимый продукт)
- Изменяется уровень автономности системы
- Нарушается Supreme Law

### Когда PROJECT_GOVERNANCE НЕ должен изменяться?

Изменение Runtime **не является основанием** для изменения PROJECT_GOVERNANCE.

Изменение конкретных технологий **не является основанием** для изменения PROJECT_GOVERNANCE.

Изменение конкретных компонентов **не является основанием** для изменения PROJECT_GOVERNANCE.

Это правило удерживает архитектуру от постепенного размывания.

---

## Change Classification

Все изменения в проекте классифицируются по трём классам. Это связывает Governance → ADR → Runtime → Implementation в единую систему управления изменениями.

### Class A: Implementation

**Что меняет:** Код, конфигурации, тесты

**Не меняет:** Документацию уровня Governance или Architecture

**Approval Level:** Runtime / Review

**Процесс:**
1. Реализация
2. Тестирование
3. Code review
4. Интеграция

**Примеры:**
- Исправление бага
- Добавление нового теста
- Оптимизация производительности
- Обновление зависимости

### Class B: Architecture

**Что меняет:** Архитектуру, доменную модель, границы системы

**Требует:** ADR (Architecture Decision Record)

**Может изменить:** Layer 2 документы (DOMAIN_ARCHITECTURE, SYSTEM_BOUNDARIES, TASK_LIFECYCLE)

**Approval Level:** Project Architect

**Процесс:**
1. Предложение изменения
2. Анализ альтернатив
3. Обоснование выбора
4. Документирование (ADR)
5. Утверждение Project Architect
6. Обновление Layer 2 документов
7. Реализация (Class A)

**Примеры:**
- Добавление новой доменной сущности
- Изменение Task Lifecycle
- Изменение границ системы
- Добавление нового сервиса

**НЕ может изменить:** PROJECT_GOVERNANCE

### Class C: Governance

**Что меняет:** Стратегию, принципы управления, архитектурные законы

**Требует:** Изменения PROJECT_GOVERNANCE

**Approval Level:** Engineering Lead

**Процесс:**
1. Предложение изменения
2. Обоснование (почему меняется стратегия)
3. Анализ влияния на все слои
4. Утверждение Engineering Lead
5. Обновление PROJECT_GOVERNANCE
6. Каскадное обновление Layer 2 и Layer 3 (если необходимо)

**Примеры:**
- Изменение Supreme Law
- Добавление нового продукта
- Изменение уровня автономности системы
- Изменение Architectural Invariants

**Только Engineering Lead имеет право инициировать Class C изменения.**

---

### Связь между классами

```
Class C (Governance)
    ↓
    может потребовать
    ↓
Class B (Architecture)
    ↓
    может потребовать
    ↓
Class A (Implementation)
```

**Обратная связь:**
- Class A **никогда** не требует Class B или C
- Class B **никогда** не требует Class C
- Class C **может** потребовать Class B и/или A

Это правило предотвращает размывание архитектуры через реализацию.

---

## Architectural Invariants

Это неизменяемые законы проекта. Они не могут быть нарушены ни при каких обстоятельствах.

### Invariant 1: Memory Repository is Single Source of Truth

**Правило:** Memory Repository — единственный источник инженерной памяти

**Обоснование:** Все архитектурные решения, знания и решения хранятся в Memory Repository.
Runtime не содержит архитектурных решений.

### Invariant 2: Runtime Does Not Contain Architectural Decisions

**Правило:** Runtime не содержит архитектурных решений

**Обоснование:** Runtime читает память проекта и выполняет её.
Runtime не принимает архитектурных решений.

### Invariant 3: Task is Primary Object

**Правило:** Task — главный объект системы

**Обоснование:** Все компоненты системы служат для продвижения Task от начала до конца.

### Invariant 4: Documentation Before Implementation

**Правило:** Documentation обновляется раньше реализации

**Обоснование:** Документация — это источник истины.
Реализация следует за документацией.

### Invariant 5: Human Approval for High Impact Decisions

**Правило:** Human Approval обязателен для High Impact решений

**Обоснование:** Соответствует Supreme Law — человек остаётся Engineering Lead.

### Invariant 6: Knowledge Item is Single Domain Entity for Knowledge

**Правило:** Knowledge Item — единственная доменная сущность знаний

**Обоснование:** Все знания представлены как Knowledge Items.
Task Memory и Project Memory — это представления Knowledge Items.

### Invariant 7: Qdrant is Index, Not Source of Truth

**Правило:** Qdrant — индекс, а не источник истины

**Обоснование:** Qdrant используется для семантического поиска,
но источником истины является Memory Repository.


---

## Decision Criteria

### Architecture Decisions

**Критерии:**
1. Независимость от реализации
2. Чёткие контракты
3. Отсутствие дублирования
4. Согласованность с Layer 2
5. Соответствие Architectural Invariants
6. Соответствие Supreme Law

**Процесс:**
1. Предложение решения
2. Анализ альтернатив
3. Обоснование выбора
4. Документирование (ADR)
5. Утверждение Project Architect

### Implementation Decisions

**Критерии:**
1. Соответствие архитектуре
2. Простота реализации
3. Тестируемость
4. Производительность
5. Соответствие Architectural Invariants

**Процесс:**
1. Анализ требований
2. Выбор подхода
3. Реализация
4. Тестирование
5. Code review
6. Интеграция

### Priority Decisions

**Критерии:**
1. Зависимости между компонентами
2. Критичность для MVP
3. Риск реализации
4. Соответствие Strategic Goals

**Процесс:**
1. Определение зависимостей
2. Оценка критичности
3. Оценка рисков
4. Определение приоритетов

---

## Deferred Decisions

Это идеи, которые не относятся к текущей фазе, но могут быть рассмотрены в будущем.

### Deferred Decision 1: Multi-agent Negotiation

**Описание:** Агенты могут вести переговоры друг с другом для решения сложных задач

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 4 или позже.

### Deferred Decision 2: Cloud Execution

**Описание:** Runtime может выполняться в облаке для масштабирования

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 4 или позже.

### Deferred Decision 3: Distributed Build

**Описание:** Сборка проекта может быть распределённой для ускорения

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 4 или позже.

### Deferred Decision 4: Marketplace

**Описание:** Marketplace для Skills, Tools, Templates

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 5 или позже.

### Deferred Decision 5: Voice Interface

**Описание:** Голосовой интерфейс для взаимодействия с агентом

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 5 или позже.

### Deferred Decision 6: Visual Workflow Editor

**Описание:** Визуальный редактор для создания Task Lifecycle

**Status:** 🚧 DEFERRED

**Причина отсрочки:** Не требуется для MVP. Может быть добавлено в Phase 5 или позже.

---

## Phase Status

| Phase | Status | Priority |
|-------|--------|----------|
| Phase 0: Architecture Foundation | ✅ COMPLETED | Critical |
| Phase 1: Strategic Planning | 🚧 IN PROGRESS | Critical |
| Phase 2: Runtime Foundation | 🚧 PLANNED | Critical |
| Phase 3: Agent Integration | 🚧 PLANNED | High |
| Phase 4: Production Ready | 🚧 FUTURE | Medium |
| Phase 5: Final Product | 🚧 FUTURE | Medium |

---

## End of Document

Этот документ определяет конституцию системы Agent Developer.

Он является главным документом проекта и имеет приоритет в вопросах стратегии, принципов управления и архитектурных законов.

### Supreme Law

> **Agent Developer максимально автоматизирует инженерную деятельность,**
> **сохраняя за человеком ответственность за стратегические решения**
> **и изменение архитектурной политики.**

### Key Principles

1. **Three Products** — три независимых продукта: memory, runtime, agent
2. **Documentation → Implementation → Verification → Knowledge Consolidation → Documentation** — цикл разработки
3. **Decision First** — сначала решения, потом код
4. **Documentation First** — документация предшествует реализации
5. **Human Approval** — подтверждение пользователя для High Impact решений
6. **Continuous Learning** — система учится на каждом завершённом проекте
7. **Evidence before Optimization** — сначала доказательства, потом оптимизация
8. **Architecture before Code** — сначала архитектура, потом код

### Architectural Invariants

1. Memory Repository is Single Source of Truth
2. Runtime Does Not Contain Architectural Decisions
3. Task is Primary Object
4. Documentation Before Implementation
5. Human Approval for High Impact Decisions
6. Knowledge Item is Single Domain Entity for Knowledge
7. Qdrant is Index, Not Source of Truth

### Governance Process

PROJECT_GOVERNANCE может быть изменён только если:
- Меняется архитектурная стратегия проекта
- Появляется новый продукт
- Изменяется уровень автономности системы
- Нарушается Supreme Law

Изменение Runtime, технологий или компонентов **не является основанием**
для изменения PROJECT_GOVERNANCE.

### Change Classification

- **Class A (Implementation):** Runtime / Review
- **Class B (Architecture):** Project Architect
- **Class C (Governance):** Engineering Lead

### Связь с другими документами

- **DOMAIN_ARCHITECTURE.md** — определяет доменную модель
- **SYSTEM_BOUNDARIES.md** — определяет границы системы
- **TASK_LIFECYCLE.md** — определяет жизненный цикл задачи
- **PROJECT_GOVERNANCE.md** (этот документ) — определяет правила развития
- **LAYER3_ROADMAP.md** — определяет план реализации Runtime

> Этот документ — конституция проекта.
> Он обеспечивает стратегический контекст на протяжении всего жизненного цикла Agent Developer.
> Все остальные документы подчиняются ему в вопросах стратегии и принципов управления.

