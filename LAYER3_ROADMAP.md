# Layer 3 Roadmap — Runtime Implementation

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-21  
**Authority:** Project Architect  
**Maintainer:** Project Architect  

**Type:** Roadmap (Layer 3: Runtime Implementation)  
**Primary Question:** "Какими итерациями строится Runtime?"  
**Canonical Source for:** Runtime components, implementation iterations, vertical slice, dependencies  
**Dependencies:** DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md, TASK_LIFECYCLE.md, PROJECT_GOVERNANCE.md  
**Dependents:** Все будущие runtime-документы и код  
**Lifecycle:** Dynamic (может часто меняться по мере реализации)

---

## Purpose

Этот документ определяет практический план реализации Runtime — исполняемой системы, которая реализует архитектурную модель из Layer 2.

Это документ реализации, а не философии. Он отвечает на вопрос: "Какими итерациями строится Runtime?"

### Что этот документ НЕ делает

- Не определяет стратегию проекта (это в PROJECT_GOVERNANCE.md)
- Не определяет доменную модель (это в DOMAIN_ARCHITECTURE.md)
- Не определяет границы системы (это в SYSTEM_BOUNDARIES.md)
- Не определяет жизненный цикл задачи (это в TASK_LIFECYCLE.md)
- Не фиксирует окончательный состав компонентов Runtime (может меняться)

### Что этот документ ДЕЛАЕТ

- Определяет начальную декомпозицию Runtime (предварительный список компонентов)
- Определяет Vertical Slice — первый работающий сценарий
- Определяет итерации реализации с Definition of Done
- Определяет зависимости между компонентами
- Определяет стратегию интеграции
- Отделяет Production Features от базового Runtime

---

## Connection to Layer 2

Runtime реализует следующие концепции из Layer 2:

### Из DOMAIN_ARCHITECTURE.md

- **Task** — главный объект системы, проходит через FSM
- **Artifact** — результат работы (код, документация, тесты)
- **Decision** — архитектурные решения (ADR)
- **Knowledge Item** — единица знания (skill, lesson, pattern)
- **Tool** — исполняемый инструмент
- **Capability** — набор возможностей (skills, tools, models, policies, templates)
- **Role** — роль агента (Architect, Planner, Coder, Reviewer, Integrator, Learning)

### Из SYSTEM_BOUNDARIES.md

- **Knowledge Service** — управление Knowledge Items
- **Memory Service** — агрегация Task/Project Memory
- **Learning Service** — извлечение знаний из задач
- **Search Service** — семантический и полнотекстовый поиск
- **Registry Service** — фасад над SkillRegistry, ToolRegistry, ReleaseRegistry
- **Execution Service** — универсальный исполнитель Tool объектов
- **Runtime Session** — контекст выполнения задачи
- **Execution Context** — состояние исполнения
- **Queues** — управление очередями задач и файлов
- **Caches** — кэширование для ускорения доступа

### Из TASK_LIFECYCLE.md

- **13 этапов** (Stage 0-12)
- **Quality Gates** для каждого этапа
- **Failure Paths** (терминальный исход любого Stage)
- **Stage Transitions** (прямые и обратные переходы)
- **7 Core Principles** (Task is Primary Object, Documentation First, Human Approval, Continuous Learning, Code is Middle, Failure is Terminal Outcome, Release is Optional)

### Из PROJECT_GOVERNANCE.md

- **Supreme Law** — Agent Developer максимально автоматизирует инженерную деятельность, сохраняя за человеком ответственность за стратегические решения
- **Architectural Invariants** — 7 неизменяемых законов
- **Operating Principles** — 7 принципов развития
- **Change Classification** — Class A (Implementation), Class B (Architecture), Class C (Governance)

---

## Начальная декомпозиция Runtime

**Важно:** Это предварительный список компонентов Runtime. Состав может меняться по мере реализации в зависимости от обнаруженных архитектурных потребностей.

Runtime состоит из следующих компонентов (предварительно):

### 1. Runtime Engine

**Ответственность:** Центральное ядро, управляющее выполнением задач.

**Что делает:**
- Управляет Task FSM (состояния: NEW, ANALYZING, PLANNING, IMPLEMENTING, REVIEWING, APPROVED, DELIVERED, COMPLETED, FAILED)
- Обрабатывает события (Event Bus)
- Координирует переходы между Stage
- Обрабатывает Failure Outcomes

**Зависимости:**
- Task (из DOMAIN_ARCHITECTURE)
- Event Model (из DOMAIN_ARCHITECTURE)
- State Model (из DOMAIN_ARCHITECTURE)

**Реализует:** Stage transitions из TASK_LIFECYCLE.md

---

### 2. FSM (Finite State Machine)

**Ответственность:** Реализация Task FSM из DOMAIN_ARCHITECTURE.md.

**Что делает:**
- Управляет состояниями Task (NEW, ANALYZING, PLANNING, IMPLEMENTING, REVIEWING, APPROVED, DELIVERED, COMPLETED, FAILED)
- Обрабатывает переходы между состояниями
- Валидирует Entry/Exit Criteria
- Обрабатывает обратные переходы

**Зависимости:**
- Task State (из DOMAIN_ARCHITECTURE)
- Event Model (из DOMAIN_ARCHITECTURE)

**Реализует:** Task FSM из DOMAIN_ARCHITECTURE.md

---

### 3. Context Manager

**Ответственность:** Управление контекстом выполнения задачи.

**Что делает:**
- Хранит Runtime Session
- Управляет открытыми документами
- Хранит временную память
- Управляет кэшем

**Зависимости:**
- Runtime Session (из SYSTEM_BOUNDARIES)
- Execution Context (из SYSTEM_BOUNDARIES)

**Реализует:** Runtime Session и Execution Context из SYSTEM_BOUNDARIES.md

---

### 4. Memory Engine

**Ответственность:** Реализация Knowledge Service и Memory Service.

**Что делает:**
- Хранит Knowledge Items
- Агрегирует Task Memory и Project Memory
- Выполняет семантический поиск (через Search Service)
- Управляет relations между Knowledge Items

**Зависимости:**
- Knowledge Item (из DOMAIN_ARCHITECTURE)
- Knowledge Service (из SYSTEM_BOUNDARIES)
- Memory Service (из SYSTEM_BOUNDARIES)
- Qdrant / SQLite (Storage)

**Реализует:** Knowledge Service и Memory Service из SYSTEM_BOUNDARIES.md

---

### 5. Capability Resolver

**Ответственность:** Реализация Stage 6 (Capability Resolution).

**Что делает:**
- Разрешает Skills (из Registry Service)
- Разрешает Tools (из Registry Service)
- Выбирает Models
- Настраивает MCP/External Services
- Применяет Policies
- Загружает Templates

**Зависимости:**
- Capability Map (из TASK_LIFECYCLE)
- Registry Service (из SYSTEM_BOUNDARIES)
- Tool (из DOMAIN_ARCHITECTURE)

**Реализует:** Stage 6 из TASK_LIFECYCLE.md

---

### 6. Execution Engine

**Ответственность:** Реализация Execution Service.

**Что делает:**
- Запускает Tool объекты
- Управляет процессами
- Собирает output/error streams
- Управляет таймаутами
- Обрабатывает ошибки

**Зависимости:**
- Execution Service (из SYSTEM_BOUNDARIES)
- Tool (из DOMAIN_ARCHITECTURE)
- ExecutionResult (из SYSTEM_BOUNDARIES)

**Реализует:** Execution Service из SYSTEM_BOUNDARIES.md

---

### 7. Agent Runtime

**Ответственность:** Выполнение агентов (Architect, Planner, Coder, Reviewer, Integrator, Learning).

**Что делает:**
- Запускает агентов для выполнения ролей
- Управляет жизненным циклом агентов
- Передаёт контекст агентам
- Собирает результаты от агентов

**Зависимости:**
- Agent (из SYSTEM_BOUNDARIES)
- Role (из DOMAIN_ARCHITECTURE)
- Runtime Session (из SYSTEM_BOUNDARIES)

**Реализует:** Agent Implementations из SYSTEM_BOUNDARIES.md

---

### 8. Orchestrator

**Ответственность:** Управление полным жизненным циклом задачи (Stage 0-12).

**Что делает:**
- Запускает Stage в правильном порядке
- Обрабатывает Quality Gates
- Обрабатывает Stage Transitions
- Координирует агентов и сервисов
- Обрабатывает Failure Paths

**Зависимости:**
- Task Lifecycle (из TASK_LIFECYCLE)
- Runtime Engine
- FSM
- Context Manager
- Memory Engine
- Capability Resolver
- Execution Engine
- Agent Runtime

**Реализует:** Task Lifecycle из TASK_LIFECYCLE.md

---

### 9. Event Bus

**Ответственность:** Доставка событий между компонентами.

**Что делает:**
- Публикует события (TaskCreated, StageCompleted, etc.)
- Подписывается на события
- Маршрутизирует события
- Гарантирует доставку

**Зависимости:**
- Event Model (из DOMAIN_ARCHITECTURE)

**Реализует:** Event Model из DOMAIN_ARCHITECTURE.md

---

### 10. Checkpoint Manager

**Ответственность:** Сохранение состояния для восстановления.

**Что делает:**
- Сохраняет checkpoint'и
- Восстанавливает из checkpoint'ов
- Управляет транзакциями
- Обеспечивает идемпотентность

**Зависимости:**
- Execution Context (из SYSTEM_BOUNDARIES)
- Runtime Session (из SYSTEM_BOUNDARIES)

**Реализует:** Runtime Session из SYSTEM_BOUNDARIES.md

---

### 11. Recovery Manager

**Ответственность:** Восстановление после сбоев.

**Что делает:**
- Обнаруживает сбои
- Восстанавливает из checkpoint'ов
- Применяет retry logic
- Обрабатывает ошибки

**Зависимости:**
- Checkpoint Manager
- Runtime Engine
- Event Bus

**Реализует:** Failure Paths из TASK_LIFECYCLE.md

---

## Vertical Slice Definition

Vertical Slice — это первый работающий сценарий, который доказывает, что архитектура работает.

### Что такое Vertical Slice?

Vertical Slice — это минимальная задача, проходящая через все слои системы:

- Domain Layer (сущности)
- System Boundaries (сервисы)
- Runtime Layer (исполнение)
- Storage Layer (хранилище)

### Определение Vertical Slice для Agent Developer

**Vertical Slice** — это минимальная задача, которая:
- Проходит через все 13 этапов (Stage 0→12)
- Создаёт хотя бы один артефакт (код, документация, тест)
- Демонстрирует работу всех ключевых компонентов
- Имеет чёткий, проверяемый результат

### Примеры Vertical Slice

**Пример 1: Hello World на Python**
- Пользователь отправляет задачу "Создать Hello World приложение на Python"
- Агент проходит через все этапы
- Создаётся файл `hello.py` с кодом
- Код выполняется успешно
- Knowledge Items создаются

**Пример 2: Простой калькулятор**
- Пользователь отправляет задачу "Создать калькулятор с базовыми операциями"
- Агент проходит через все этапы
- Создаётся файл `calculator.py` с кодом
- Тесты проходят
- Knowledge Items создаются

**Пример 3: Документация**
- Пользователь отправляет задачу "Создать README для проекта"
- Агент проходит через все этапы
- Создаётся файл `README.md`
- Документация проверяется
- Knowledge Items создаются

### Критерии успеха Vertical Slice

- ✅ Задача проходит через все 13 этапов
- ✅ Артефакт создаётся и сохраняется
- ✅ Артефакт проверяется (тесты, валидация)
- ✅ Knowledge Items создаются
- ✅ Decision Records сохраняются (если были приняты решения)
- ✅ Пользователь может подтвердить результат

### Почему Vertical Slice важен?

- Доказывает полноту реализации (все этапы работают)
- Демонстрирует интеграцию компонентов
- Даёт базу для расширения до более сложных сценариев
- Позволяет обнаружить архитектурные проблемы на раннем этапе

### Что Vertical Slice НЕ делает?

- Не реализует все возможности (только минимум)
- Не оптимизирует производительность
- Не обрабатывает все edge cases
- Не реализует все агентов (только необходимых для минимального сценария)

---

## Implementation Iterations

Runtime реализуется итерациями. Каждая итерация имеет чёткое Definition of Done.

### Iteration 1: Core Foundation + Event Bus

**Цель:** Создать базовую инфраструктуру для Runtime с Event Bus для decoupling.

**Компоненты:**
- Runtime Engine (базовый)
- FSM (базовый)
- **Event Bus (базовый)** — для decoupling Runtime Engine и FSM
- Context Manager (базовый)

**Почему Event Bus нужен сразу:**
- Runtime Engine и FSM не должны быть сильно связаны
- События — это основной механизм коммуникации между компонентами
- Event Bus позволяет добавлять новые компоненты без изменения существующих

**Definition of Done:**
- ✅ Runtime Engine может создавать Task
- ✅ FSM может управлять состояниями Task
- ✅ **Event Bus публикует и доставляет события**
- ✅ Context Manager может хранить Runtime Session
- ✅ Task может переходить между состояниями
- ✅ Базовые тесты проходят

**Результат:** Базовая инфраструктура с Event Bus готова

---

### Iteration 2: Memory Integration

**Цель:** Интегрировать Memory Engine для работы с Knowledge Items.

**Компоненты:**
- Memory Engine
- Integration with Qdrant / SQLite

**Definition of Done:**
- ✅ Memory Engine может сохранять Knowledge Items
- ✅ Memory Engine может извлекать Knowledge Items
- ✅ Семантический поиск работает
- ✅ Task Memory агрегируется
- ✅ Project Memory обновляется
- ✅ Интеграционные тесты проходят

**Результат:** Memory Engine интегрирован

---

### Iteration 3: Execution Engine

**Цель:** Реализовать Execution Engine для запуска Tools.

**Компоненты:**
- Execution Engine
- Tool Registry integration

**Definition of Done:**
- ✅ Execution Engine может запускать Tools
- ✅ Output/error streams собираются
- ✅ Таймауты обрабатываются
- ✅ Ошибки обрабатываются
- ✅ ExecutionResult возвращается
- ✅ Интеграционные тесты проходят

**Результат:** Execution Engine работает

---

### Iteration 4: Capability Resolver

**Цель:** Реализовать Capability Resolver для Stage 6.

**Компоненты:**
- Capability Resolver
- Registry Service integration

**Definition of Done:**
- ✅ Capability Resolver может разрешать Skills
- ✅ Capability Resolver может разрешать Tools
- ✅ Capability Map создаётся
- ✅ Fallback определяется
- ✅ Интеграционные тесты проходят

**Результат:** Capability Resolver работает

---

### Iteration 5: Agent Runtime

**Цель:** Реализовать Agent Runtime для выполнения агентов.

**Компоненты:**
- Agent Runtime
- Integration with LLM (Qwen)

**Definition of Done:**
- ✅ Agent Runtime может запускать агентов
- ✅ Агенты могут выполнять роли
- ✅ Контекст передаётся агентам
- ✅ Результаты собираются
- ✅ Интеграционные тесты проходят

**Результат:** Agent Runtime работает

---

### Iteration 6: Orchestrator

**Цель:** Реализовать Orchestrator для управления Task Lifecycle.

**Компоненты:**
- Orchestrator
- Integration with all components

**Definition of Done:**
- ✅ Orchestrator может запускать Stage
- ✅ Quality Gates обрабатываются
- ✅ Stage Transitions работают
- ✅ Failure Paths обрабатываются
- ✅ **Vertical Slice проходит полностью**
- ✅ Интеграционные тесты проходят

**Результат:** **Vertical Slice работает** — базовый Runtime готов

---

## Production Features

Следующие компоненты не являются частью базового Runtime, но необходимы для production-ready системы.

Они реализуются **после успешного Vertical Slice**.

### Production Feature 1: Checkpoint Manager

**Ответственность:** Сохранение состояния для восстановления.

**Что делает:**
- Сохраняет checkpoint'и
- Восстанавливает из checkpoint'ов
- Управляет транзакциями
- Обеспечивает идемпотентность

**Зависимости:**
- Execution Context (из SYSTEM_BOUNDARIES)
- Runtime Session (из SYSTEM_BOUNDARIES)

**Когда реализуется:** После Vertical Slice

---

### Production Feature 2: Recovery Manager

**Ответственность:** Восстановление после сбоев.

**Что делает:**
- Обнаруживает сбои
- Восстанавливает из checkpoint'ов
- Применяет retry logic
- Обрабатывает ошибки

**Зависимости:**
- Checkpoint Manager
- Runtime Engine
- Event Bus

**Когда реализуется:** После Checkpoint Manager

---

### Production Features Success Criteria

Production Features считаются готовыми, если:

- ✅ Checkpoint'и сохраняются
- ✅ Восстановление из checkpoint'ов работает
- ✅ Retry logic работает
- ✅ Система устойчива к сбоям
- ✅ Интеграционные тесты проходят

**Результат:** Production-ready Runtime

---

## Dependencies Graph

Зависимости между компонентами:

    Orchestrator
        ↓
    Runtime Engine
        ↓
        ├── FSM
        ├── Context Manager
        ├── Memory Engine
        ├── Capability Resolver
        ├── Execution Engine
        └── Agent Runtime

    Event Bus (cross-cutting с самого начала)
        ↓
        └── Все компоненты

    Production Features (после Vertical Slice):
    Checkpoint Manager
        ↓
    Recovery Manager

### Критические пути

**Критический путь 1:** Runtime Engine → FSM → Orchestrator

**Критический путь 2:** Memory Engine → Capability Resolver → Agent Runtime

**Критический путь 3:** Execution Engine → Agent Runtime → Orchestrator

---

## Integration Strategy

### Стратегия интеграции

Интеграция компонентов происходит итеративно:

1. **Iteration 1:** Базовая инфраструктура + Event Bus (Runtime Engine, FSM, Event Bus, Context Manager)
2. **Iteration 2-3:** Интеграция сервисов (Memory Engine, Execution Engine)
3. **Iteration 4-5:** Интеграция возможностей (Capability Resolver, Agent Runtime)
4. **Iteration 6:** Оркестрация (Orchestrator) — **Vertical Slice**
5. **Production Features:** Надёжность (Checkpoint Manager, Recovery Manager)

### Принципы интеграции

1. **Инкрементальность** — каждый компонент интегрируется отдельно
2. **Тестируемость** — каждый компонент тестируется независимо
3. **Обратная совместимость** — новые версии не ломают старые
4. **Документированность** — каждый компонент документируется
5. **Decoupling через Event Bus** — компоненты не должны быть сильно связаны

### Стратегия тестирования

1. **Unit tests** — для каждого компонента
2. **Integration tests** — для взаимодействия компонентов
3. **End-to-end tests** — для Vertical Slice
4. **Performance tests** — для производительности (в Production Features)

---

## Deferred Items

Следующие возможности откладываются до более поздних итераций (после Production Features):

### Deferred Item 1: Multi-agent Negotiation

**Описание:** Агенты могут вести переговоры друг с другом

**Причина отсрочки:** Не требуется для Vertical Slice или Production Features

### Deferred Item 2: Cloud Execution

**Описание:** Runtime может выполняться в облаке

**Причина отсрочки:** Не требуется для Vertical Slice или Production Features

### Deferred Item 3: Distributed Build

**Описание:** Сборка проекта может быть распределённой

**Причина отсрочки:** Не требуется для Vertical Slice или Production Features

### Deferred Item 4: Marketplace

**Описание:** Marketplace для Skills, Tools, Templates

**Причина отсрочки:** Не требуется для Vertical Slice или Production Features

### Deferred Item 5: Visual Workflow Editor

**Описание:** Визуальный редактор для создания Task Lifecycle

**Причина отсрочки:** Не требуется для Vertical Slice или Production Features

---

## Success Criteria

### Iteration Success Criteria

Каждая итерация считается успешной, если:

- ✅ Definition of Done выполнено
- ✅ Все тесты проходят
- ✅ Документация обновлена
- ✅ Код прошёл code review
- ✅ Интеграция с предыдущими итерациями работает

### Vertical Slice Success Criteria

Vertical Slice считается успешным, если:

- ✅ Задача проходит через все 13 этапов
- ✅ Артефакт создаётся и сохраняется
- ✅ Артефакт проверяется (тесты, валидация)
- ✅ Knowledge Items создаются
- ✅ Decision Records сохраняются (если были приняты решения)
- ✅ Пользователь может подтвердить результат

### Production Features Success Criteria

Production Features считаются готовыми, если:

- ✅ Checkpoint'и сохраняются
- ✅ Восстановление из checkpoint'ов работает
- ✅ Retry logic работает
- ✅ Система устойчива к сбоям
- ✅ Интеграционные тесты проходят

### Runtime Success Criteria

Runtime считается успешным, если:

- ✅ Может выполнять Task Lifecycle от Stage 0 до Stage 12
- ✅ Агенты могут выполнять свои роли
- ✅ Tools могут выполняться
- ✅ Knowledge Retrieval работает
- ✅ Система устойчива к сбоям (Production Features готовы)

---

## End of Document

Этот документ определяет практический план реализации Runtime — исполняемой системы, которая реализует архитектурную модель из Layer 2.

Это мост между архитектурой и кодом.

### Ключевые принципы

1. **Практичность** — документ реализации, а не философии
2. **Итеративность** — реализация идёт итерациями с чёткими Definition of Done
3. **Vertical Slice First** — первый приоритет — работающий сценарий
4. **Тестируемость** — каждый компонент тестируется независимо
5. **Инкрементальность** — каждый компонент интегрируется отдельно
6. **Гибкость** — состав компонентов Runtime может меняться по мере реализации
7. **Decoupling через Event Bus** — Event Bus введён рано для предотвращения сильной связности
8. **Production Features отдельно** — надёжность явно отделена от базового Runtime

### Связь с другими документами

- **DOMAIN_ARCHITECTURE.md** — определяет доменную модель
- **SYSTEM_BOUNDARIES.md** — определяет границы системы
- **TASK_LIFECYCLE.md** — определяет жизненный цикл задачи
- **PROJECT_GOVERNANCE.md** — определяет стратегию развития
- **LAYER3_ROADMAP.md** (этот документ) — определяет план реализации Runtime

> Этот документ — мост между архитектурой и кодом.
> Он обеспечивает практический план реализации Runtime.

