# System Boundaries

**Status:** ACCEPTED  
**Version:** 1.0  
**Date:** 2026-06-21  
**Authority:** Project Architect  
**Maintainer:** Architecture Maintainer  

**Type:** Architecture (Layer 2: Operational Knowledge)  
**Primary Question:** "Каковы границы системы и как реализуются доменные сущности?"  
**Canonical Source for:** Services, Runtime, Storage, Projections, Agent implementations  
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md, DOMAIN_ARCHITECTURE.md  
**Dependents:** TASK_LIFECYCLE.md, все будущие runtime-компоненты  
**Lifecycle:** Semi-static (может изменяться по мере эволюции реализации)

---

## Purpose

Этот документ определяет границы системы Agent Developer и описывает, как реализуются доменные сущности из DOMAIN_ARCHITECTURE.md.

System Boundaries — это мост между доменной моделью (что есть) и реализацией (как работает).

### Связь с Domain Architecture

DOMAIN_ARCHITECTURE.md определяет **вечные сущности**:
- Portfolio, Project, Task, Workspace
- Artifact, Decision, Skill, Tool, Knowledge Item, Release
- Event, State, Role

SYSTEM_BOUNDARIES.md определяет **реализацию**:
- Сервисы для работы с сущностями
- Runtime для выполнения задач
- Storage для хранения данных
- Projections для представления данных

### Architecture Law #1

> **Если сущность перестаёт существовать при замене runtime, orchestration engine или storage, то она не принадлежит Domain Architecture.**

Этот документ описывает именно те сущности, которые **могут быть заменены**:
- Сервисы могут быть переписаны
- Runtime может быть заменён (LangGraph → Temporal → другой orchestrator)
- Storage может быть изменён (SQLite → PostgreSQL → другое хранилище)
- Projections могут быть изменены (Markdown → JSON → другой формат)

Но доменные сущности (Task, Decision, Artifact) остаются неизменными.

### Future Evolution Note

> **v2 Evolution:** Execution Service планируется эволюционировать от `execute(tool: Tool, args)` к `execute(request: ExecutionRequest)`, где ExecutionRequest содержит tool, args, sandbox, env, cwd, stdin, timeout, resource limits, telemetry. Это позволит расширять возможности исполнения без изменения контракта.

---

## Four-Level Architecture (Reminder)

Архитектура системы разделена на четыре независимых уровня:

**Уровень 1: DOMAIN ARCHITECTURE (вечные сущности)**
- Portfolio, Project, Task, Workspace
- Artifact, Decision, Skill, Tool, Knowledge Item, Release
- Event, State, Role
- Описывается в DOMAIN_ARCHITECTURE.md

**Уровень 2: SYSTEM BOUNDARIES (сервисы)**
- Knowledge Service, Memory Service, Learning Service
- Search Service, Registry Service, Execution Service
- Описывается в этом документе

**Уровень 3: RUNTIME (исполнение)**
- Runtime Session, Execution Context
- Queues, Caches, Agents
- Описывается в этом документе

**Уровень 4: STORAGE (носители)**
- Markdown, JSON, SQLite, Qdrant, Git
- Описывается в этом документе


---

## Services Layer

Сервисы — это компоненты, которые обеспечивают работу с доменными сущностями.

Каждый сервис имеет чёткий контракт (набор методов) и может быть реализован по-разному.

### Knowledge Service

**Purpose:** Управление Knowledge Items (единицами знаний).

**Responsibilities:**
- Создание Knowledge Items
- Обновление Knowledge Items
- Поиск Knowledge Items (по тегам, категориям)
- Связывание Knowledge Items (relations)
- Управление confidence

**Contract:**

    interface KnowledgeService {
      createKnowledgeItem(item: KnowledgeItem): Promise<void>
      updateKnowledgeItem(id: string, updates: Partial<KnowledgeItem>): Promise<void>
      getKnowledgeItem(id: string): Promise<KnowledgeItem | null>
      searchKnowledgeItems(query: SearchQuery): Promise<KnowledgeItem[]>
      addRelation(fromId: string, toId: string): Promise<void>
      removeRelation(fromId: string, toId: string): Promise<void>
      updateConfidence(id: string, confidence: number): Promise<void>
    }

**Implementation Options:**
- SQLite + FTS5 для полнотекстового поиска
- Qdrant для векторного поиска (embedding)
- Комбинация SQLite + Qdrant

---

### Memory Service

**Purpose:** Агрегация Knowledge Items в Task Memory и Project Memory.

**Responsibilities:**
- Создание Task Memory (агрегация Knowledge Items задачи)
- Создание Project Memory (агрегация Knowledge Items проекта)
- Обновление Memory при создании новых Knowledge Items
- Предоставление Memory для чтения

**Contract:**

    interface MemoryService {
      createTaskMemory(taskId: string): Promise<void>
      createProjectMemory(projectId: string): Promise<void>
      updateTaskMemory(taskId: string, knowledgeItemId: string): Promise<void>
      updateProjectMemory(projectId: string, knowledgeItemId: string): Promise<void>
      getTaskMemory(taskId: string): Promise<MemoryView>
      getProjectMemory(projectId: string): Promise<MemoryView>
    }

**Memory View:**

    interface MemoryView {
      id: string
      type: "task" | "project"
      knowledge_items: KnowledgeItem[]
      summary: string
      last_updated: string
    }

**Implementation Options:**
- SQLite для хранения агрегированных представлений
- In-memory cache для быстрого доступа
- Materialized views для оптимизации

---

### Learning Service

**Purpose:** Извлечение знаний из задач и консолидация.

**Responsibilities:**
- Анализ завершённых задач
- Извлечение lessons learned
- Предложение skill candidates
- Анализ метрик и benchmarks
- Обновление confidence Knowledge Items

**Contract:**

    interface LearningService {
      analyzeTask(taskId: string): Promise<LearningResult>
      extractLessons(taskId: string): Promise<KnowledgeItem[]>
      proposeSkillCandidates(taskId: string): Promise<SkillCandidate[]>
      analyzeMetrics(taskId: string): Promise<MetricsAnalysis>
      consolidateKnowledge(projectId: string): Promise<void>
    }

**Implementation Options:**
- Rule-based extraction (шаблоны для lessons)
- LLM-based extraction (анализ с помощью модели)
- Statistical analysis (для метрик)

---

### Search Service

**Purpose:** Семантический поиск Knowledge Items.

**Responsibilities:**
- Векторный поиск (по embedding)
- Полнотекстовый поиск (по тегам, категориям)
- Фильтрация по проекту, задаче, типу
- Ранжирование результатов

**Contract:**

    interface SearchService {
      semanticSearch(query: string, filters?: SearchFilters): Promise<KnowledgeItem[]>
      fullTextSearch(query: string, filters?: SearchFilters): Promise<KnowledgeItem[]>
      hybridSearch(query: string, filters?: SearchFilters): Promise<KnowledgeItem[]>
    }

**Implementation Options:**
- Qdrant для векторного поиска
- SQLite FTS5 для полнотекстового поиска
- Комбинация с весами для hybrid search

---

### Registry Service

**Purpose:** Фасад над тремя специализированными реестрами (Skill, Tool, Release).

**Architectural Decision:** Registry Service реализует паттерн Facade. Внутри он делегирует операции трём специализированным реестрам (SkillRegistry, ToolRegistry, ReleaseRegistry), что соблюдает Single Responsibility Principle.

**Responsibilities:**
- Единая точка доступа для агентов
- Делегирование операций специализированным реестрам
- Управление статусами (CANDIDATE, APPROVED, DEPRECATED)
- Подсчёт usage_count, success_rate

**Internal Structure:**

    RegistryService (Facade)
        ├── SkillRegistry (internal)
        ├── ToolRegistry (internal)
        └── ReleaseRegistry (internal)

**Contract:**

    interface RegistryService {
      // Skills (делегирование SkillRegistry)
      createSkill(skill: Skill): Promise<void>
      updateSkill(id: string, updates: Partial<Skill>): Promise<void>
      getSkill(id: string): Promise<Skill | null>
      listSkills(filters?: SkillFilters): Promise<Skill[]>
      
      // Tools (делегирование ToolRegistry)
      createTool(tool: Tool): Promise<void>
      updateTool(id: string, updates: Partial<Tool>): Promise<void>
      getTool(id: string): Promise<Tool | null>
      listTools(filters?: ToolFilters): Promise<Tool[]>
      
      // Releases (делегирование ReleaseRegistry)
      createRelease(release: Release): Promise<void>
      updateRelease(id: string, updates: Partial<Release>): Promise<void>
      getRelease(id: string): Promise<Release | null>
      listReleases(projectId: string): Promise<Release[]>
      
      // Skill Candidates
      createSkillCandidate(candidate: SkillCandidate): Promise<void>
      approveSkillCandidate(id: string): Promise<Skill>
      rejectSkillCandidate(id: string): Promise<void>
    }

**Implementation Options:**
- SQLite для хранения трёх реестров
- JSON files для простых случаев
- In-memory cache для быстрого доступа

---

### Execution Service

**Purpose:** Универсальный исполнитель команд и инструментов.

**Architectural Decision:** Execution Service не знает о Registry Service. Он принимает готовый Tool объект, что делает его полностью независимым от реестра и универсальным исполнителем.

**Responsibilities:**
- Запуск исполняемых файлов (flutter, dart, git, etc.)
- Управление процессами
- Сбор output и error streams
- Управление таймаутами
- Обработка ошибок

**Contract:**

    interface ExecutionService {
      executeTool(tool: Tool, args: string[], options?: ExecutionOptions): Promise<ExecutionResult>
      executeCommand(command: string, args: string[], options?: ExecutionOptions): Promise<ExecutionResult>
      cancelExecution(executionId: string): Promise<void>
    }

**Execution Result:**

    interface ExecutionResult {
      execution_id: string
      tool_id: string
      exit_code: number
      stdout: string
      stderr: string
      duration_ms: number
      status: "SUCCESS" | "FAILED" | "TIMEOUT" | "CANCELLED"
    }

**Implementation Options:**
- Node.js child_process
- Python subprocess
- Docker containers для изоляции


---

## Runtime Layer

Runtime — это компоненты, которые обеспечивают выполнение задач.

Runtime может быть полностью заменён без изменения доменной модели.

### Runtime Session

**Purpose:** Контекст выполнения задачи.

**Responsibilities:**
- Хранение контекста модели (tokens, context window)
- Управление открытыми документами
- Хранение активных ролей
- Управление кэшем (skills, tools)
- Управление очередями файлов
- Хранение временной памяти

**Contract:**

    interface RuntimeSession {
      id: string
      task_id: string
      started_at: string
      ended_at?: string
      status: "ACTIVE" | "PAUSED" | "COMPLETED" | "FAILED"
      
      // Model context
      model_context: ModelContext
      
      // Open documents
      open_documents: string[]
      
      // Active roles
      active_roles: string[]
      
      // Caches
      skill_cache: string[]
      tool_cache: string[]
      
      // Queues
      pending_files: string[]
      completed_files: string[]
      
      // Temporary memory
      temporary_memory: TemporaryMemory
      
      // Methods
      addOpenDocument(path: string): void
      removeOpenDocument(path: string): void
      addSkillToCache(skillId: string): void
      addToolToCache(toolId: string): void
      addFileToQueue(fileId: string): void
      markFileCompleted(fileId: string): void
      saveTemporaryMemory(key: string, value: any): void
      getTemporaryMemory(key: string): any
    }

**Implementation Options:**
- In-memory для коротких сессий
- Redis для распределённых сессий
- Database для персистентных сессий

---

### Execution Context

**Purpose:** Состояние исполнения на конкретный момент времени.

**Responsibilities:**
- Хранение текущего состояния задачи
- Хранение промежуточных результатов
- Управление транзакциями
- Обеспечение идемпотентности

**Contract:**

    interface ExecutionContext {
      task_id: string
      current_stage: number
      current_state: string
      artifacts: Artifact[]
      decisions: Decision[]
      
      // Methods
      saveState(): Promise<void>
      restoreState(): Promise<void>
      commitTransaction(): Promise<void>
      rollbackTransaction(): Promise<void>
    }

**Implementation Options:**
- In-memory для простых случаев
- Database для сложных транзакций
- Event sourcing для аудита

---

### Queues

**Purpose:** Управление очередями задач и файлов.

**Responsibilities:**
- Очередь задач (Task Queue)
- Очередь файлов (File Queue)
- Очередь событий (Event Queue)
- Приоритизация
- Retry logic

**Contract:**

    interface QueueService {
      // Task Queue
      enqueueTask(taskId: string, priority: number): Promise<void>
      dequeueTask(): Promise<string | null>
      
      // File Queue
      enqueueFile(taskId: string, fileId: string, priority: number): Promise<void>
      dequeueFile(taskId: string): Promise<string | null>
      
      // Event Queue
      enqueueEvent(event: Event): Promise<void>
      dequeueEvent(): Promise<Event | null>
    }

**Implementation Options:**
- In-memory queues для простых случаев
- Redis queues для распределённых систем
- Database queues для персистентности

---

### Caches

**Purpose:** Кэширование для ускорения доступа.

**Responsibilities:**
- Кэш Knowledge Items
- Кэш Skill
- Кэш Tool
- Кэш конфигурации
- Invalidation logic

**Contract:**

    interface CacheService {
      get<T>(key: string): Promise<T | null>
      set<T>(key: string, value: T, ttl?: number): Promise<void>
      delete(key: string): Promise<void>
      invalidate(pattern: string): Promise<void>
    }

**Implementation Options:**
- In-memory cache (Map) для простых случаев
- Redis для распределённых систем
- LRU cache для ограничения размера


---

## Agent Implementations

Агенты — это runtime-исполнители ролей из доменной модели.

Каждый агент реализует определённую роль и имеет доступ к определённым сервисам.

**Важно:** Agent — это runtime-сущность, не доменная. В доменной модели есть только Role (см. DOMAIN_ARCHITECTURE.md). Агенты — это конкретные исполнители, которые могут быть заменены (LLM-агент, человек, другой фреймворк).

### Architect Agent

**Role:** Architect

**Responsibilities:**
- Анализ требований
- Принятие архитектурных решений
- Создание Decision Records
- Обоснование выбора технологий

**Allowed Services:**
- Knowledge Service (read)
- Memory Service (read/write)
- Registry Service (read)

**Outputs:**
- Decision Records
- Architecture decisions

**Implementation:**
- LLM-based agent с промптом для анализа
- Доступ к Project Memory для контекста
- Создание Decision Records через Registry Service

---

### Planner Agent

**Role:** Planner

**Responsibilities:**
- Создание плана реализации
- Определение порядка файлов
- Оценка усилий
- Приоритизация задач

**Allowed Services:**
- Knowledge Service (read)
- Memory Service (read)
- Registry Service (read)

**Outputs:**
- Implementation Plan
- Project Manifest
- File dependencies

**Implementation:**
- LLM-based agent с промптом для планирования
- Анализ Implementation Plan из DOMAIN_ARCHITECTURE.md
- Создание project_manifest.json и implementation_plan.json

---

### Coder Agent

**Role:** Coder

**Responsibilities:**
- Написание кода
- Написание тестов
- Исправление багов
- Предложение skill candidates

**Allowed Services:**
- Knowledge Service (read)
- Memory Service (read)
- Registry Service (read/write для skill candidates)
- Execution Service (для запуска тестов, принимает Tool объект)

**Workflow (с учётом архитектурных решений):**

    1. Coder Agent получает задачу
    2. Получает Skill из Registry Service
    3. Получает Tool из Registry Service (Tool объект)
    4. Передаёт Tool в ExecutionService.executeTool(tool, args)
    5. Получает ExecutionResult
    6. Предлагает skill candidates при обнаружении хороших паттернов

**Важно:** Execution Service не знает о Registry Service. Coder Agent сам получает Tool из Registry и передаёт его в Execution Service.

**Outputs:**
- Code files
- Test files
- Skill Candidates

**Implementation:**
- LLM-based agent с промптом для написания кода
- Доступ к Skill из Registry Service
- Получение Tool из Registry Service
- Запуск тестов через Execution Service (передаёт Tool объект)
- Предложение skill candidates при обнаружении хороших паттернов

---

### Reviewer Agent

**Role:** Reviewer

**Responsibilities:**
- Ревью кода
- Проверка качества
- Предложение улучшений
- Одобрение или отклонение

**Allowed Services:**
- Knowledge Service (read)
- Memory Service (read)
- Execution Service (для запуска линтеров, анализаторов)

**Workflow:**

    1. Reviewer Agent получает код на ревью
    2. Получает Tool (линтер, анализатор) из Registry Service
    3. Передаёт Tool в ExecutionService.executeTool(tool, args)
    4. Анализирует результаты
    5. Формирует review report

**Outputs:**
- Review reports
- Quality metrics
- Improvement suggestions

**Implementation:**
- LLM-based agent с промптом для ревью
- Запуск статического анализа через Execution Service
- Проверка соответствия architectural decisions

---

### Integrator Agent

**Role:** Integrator

**Responsibilities:**
- Интеграция кода
- Запуск интеграционных тестов
- Валидация архитектуры
- Проверка circular dependencies

**Allowed Services:**
- Knowledge Service (read)
- Memory Service (read)
- Execution Service (для запуска тестов)

**Workflow:**

    1. Integrator Agent получает интегрируемый код
    2. Получает Tool (test runner) из Registry Service
    3. Передаёт Tool в ExecutionService.executeTool(tool, args)
    4. Анализирует зависимости
    5. Формирует integration report

**Outputs:**
- Integration reports
- Dependency validation results
- Architecture compliance reports

**Implementation:**
- LLM-based agent с промптом для интеграции
- Запуск интеграционных тестов через Execution Service
- Анализ зависимостей

---

### Learning Agent

**Role:** Learning

**Responsibilities:**
- Извлечение lessons learned
- Анализ метрик
- Предложение skill candidates
- Консолидация знаний

**Allowed Services:**
- Knowledge Service (read/write)
- Memory Service (read/write)
- Registry Service (read/write)
- Learning Service (использует напрямую)

**Workflow:**

    1. Learning Agent получает завершённую задачу
    2. Анализирует артефакты и решения
    3. Извлекает lessons learned через Learning Service
    4. Предлагает skill candidates
    5. Обновляет Knowledge Items
    6. Консолидирует знания в Project Memory

**Outputs:**
- Lessons learned
- Skill candidates
- Quality metrics
- Benchmark results

**Implementation:**
- LLM-based agent с промптом для анализа
- Использование Learning Service для извлечения знаний
- Обновление Knowledge Items через Knowledge Service


---

## Storage Layer

Storage — это носители данных.

Storage может быть полностью заменён без изменения доменной модели или сервисов.

### Markdown

**Purpose:** Хранение текстовых артефактов и документов.

**Use Cases:**
- Artifact: requirements_report.md, engineering_spec.md
- Decision: DR-001-state-management.md
- Memory: tasks/{task_id}/memory.md
- Documentation: DOMAIN_ARCHITECTURE.md

**Implementation:**
- File system
- Git для версионирования

**Advantages:**
- Human-readable
- Version control friendly
- Easy to edit manually

**Limitations:**
- No query capabilities
- No structured search
- Manual parsing required

---

### JSON

**Purpose:** Хранение структурированных данных.

**Use Cases:**
- Contracts: Task, Artifact, Decision
- Manifests: project_manifest.json, implementation_plan.json
- Configuration: skill_map.json

**Implementation:**
- File system
- Database (JSONB column)

**Advantages:**
- Structured data
- Easy parsing
- Schema validation possible

**Limitations:**
- Not human-readable for large files
- No query capabilities (without database)
- Manual versioning

---

### SQLite

**Purpose:** Хранение сущностей с возможностью запросов.

**Use Cases:**
- Knowledge Items (с FTS5 для полнотекстового поиска)
- Skills, Tools, Releases (через Registry Service)
- Tasks, Projects (для быстрого доступа)

**Implementation:**
- SQLite database
- FTS5 extension для полнотекстового поиска

**Advantages:**
- Full SQL query capabilities
- Fast reads
- Transaction support
- FTS5 for full-text search

**Limitations:**
- Single-writer limitation
- Not suitable for distributed systems
- Requires schema management

---

### Qdrant

**Purpose:** Векторное хранилище для семантического поиска.

**Use Cases:**
- Knowledge Items embedding
- Semantic search

**Implementation:**
- Qdrant vector database
- Embedding models для генерации векторов

**Advantages:**
- Fast vector similarity search
- Scalable
- Filtering support

**Limitations:**
- Requires embedding generation
- Additional infrastructure
- Not suitable for exact matches

---

### Git

**Purpose:** Версионирование документов и кода.

**Use Cases:**
- Documentation versioning
- Code versioning
- Release tags

**Implementation:**
- Git repository
- Branches для задач
- Tags для релизов

**Advantages:**
- Full version history
- Branching and merging
- Distributed
- Industry standard

**Limitations:**
- Not suitable for binary data
- Requires Git knowledge
- Manual conflict resolution


---

## Projection Layer

Projection — это форма представления доменной сущности.

Одна сущность может иметь несколько проекций.

### Document as Projection

Document — это не доменная сущность, а форма представления.

**Examples:**
- Decision → DR-001.md (Markdown projection)
- Task → task-001.json (JSON projection)
- Knowledge Item → knowledge-001.json (JSON projection)
- Memory → memory.md (Markdown projection)

**Implementation:**
- Serializers для преобразования сущностей в проекции
- Deserializers для преобразования проекций в сущности

**Why Projection Matters:**
- Одна сущность может быть представлена в разных форматах
- Разные потребители могут требовать разные форматы
- Хранилище может меняться без изменения доменной модели
- API может возвращать JSON, а файл — Markdown

---

## Data Flow

Как данные движутся между слоями:

### Task Execution Flow

    User
      ↓
    [Task Created] → Task (Domain)
      ↓
    [Task Queued] → Queue Service (System Boundary)
      ↓
    [Task Started] → Runtime Session (Runtime)
      ↓
    [Stage 1: Analysis] → Knowledge Service (System Boundary)
      ↓
    [Knowledge Retrieved] → Knowledge Items (Domain)
      ↓
    [Stage 4: Architecture] → Decision Created
      ↓
    [Decision Stored] → Registry Service (System Boundary)
      ↓
    [Stage 7: Development] → Coder Agent (Runtime)
      ↓
    [Get Tool from Registry] → Tool (Domain)
      ↓
    [Execute Tool] → Execution Service (System Boundary)
      ↓
    [Code Written] → Artifact (Domain)
      ↓
    [Artifact Stored] → Storage (Markdown/JSON)
      ↓
    [Stage 12: Learning] → Learning Service (System Boundary)
      ↓
    [Knowledge Extracted] → Knowledge Items (Domain)
      ↓
    [Knowledge Stored] → Qdrant/SQLite (Storage)

### Tool Execution Flow (Архитектурно важный)

Этот flow демонстрирует ключевое архитектурное решение: Execution Service не зависит от Registry Service.

    Agent needs to execute tool
      ↓
    [1. Get Tool] → Registry Service.getTool(toolId)
      ↓
    [2. Return Tool object] → Tool (Domain entity)
      ↓
    [3. Execute Tool] → ExecutionService.executeTool(tool, args)
      ↓
    [4. Run executable] → Process (Runtime)
      ↓
    [5. Return result] → ExecutionResult
      ↓
    [6. Result returned] → Agent (Runtime)

**Ключевые моменты:**
- Шаг 1-2: Агент получает Tool объект из Registry Service
- Шаг 3: Агент передаёт Tool объект в Execution Service
- Execution Service не знает о Registry Service
- Execution Service не знает о toolId, он работает с Tool объектом
- Это позволяет заменить Registry Service без изменения Execution Service

### Knowledge Retrieval Flow

    Agent needs knowledge
      ↓
    [Search Request] → Search Service (System Boundary)
      ↓
    [Semantic Search] → Qdrant (Storage)
      ↓
    [Full Text Search] → SQLite FTS5 (Storage)
      ↓
    [Results Combined] → Knowledge Items (Domain)
      ↓
    [Results Returned] → Agent (Runtime)

### Memory Aggregation Flow

    Task completed
      ↓
    [Aggregate Knowledge] → Memory Service (System Boundary)
      ↓
    [Collect Knowledge Items] → Knowledge Service (System Boundary)
      ↓
    [Create Memory View] → Memory (Domain concept)
      ↓
    [Store Memory] → SQLite/JSON (Storage)

---

## Service Contracts Summary

Все сервисы должны следовать этим принципам:

### Interface Segregation

Каждый сервис имеет чёткий интерфейс с минимальным набором методов.

**Пример:**
- Knowledge Service не содержит методов для управления Skills
- Registry Service не содержит методов для выполнения кода
- Execution Service не содержит методов для поиска знаний

### Dependency Inversion

Сервисы зависят от абстракций (интерфейсов), а не от реализаций.

**Пример:**
- Coder Agent зависит от интерфейса ExecutionService, а не от конкретной реализации
- Execution Service зависит от интерфейса Tool (доменная сущность), а не от Registry Service
- Это позволяет заменить реализацию без изменения агентов

### Single Responsibility

Каждый сервис отвечает за одну область:
- Knowledge Service → Knowledge Items
- Memory Service → Memory aggregation
- Learning Service → Knowledge extraction
- Search Service → Knowledge search
- Registry Service → Skill/Tool/Release storage (фасад)
- Execution Service → Tool execution

### Open/Closed Principle

Сервисы открыты для расширения, но закрыты для модификации.

Новые реализации могут быть добавлены без изменения контракта.

**Пример:**
- Можно добавить новую реализацию Knowledge Service (например, Elasticsearch) без изменения интерфейса
- Можно добавить новую реализацию Execution Service (например, Docker-based) без изменения интерфейса

### Separation of Concerns

Разделение ответственности между слоями:
- Domain Layer → вечные сущности (не меняются)
- System Boundaries → сервисы (могут меняться)
- Runtime → исполнение (может меняться)
- Storage → носители (могут меняться)

**Пример:**
- Если меняется хранилище (SQLite → PostgreSQL), меняются только сервисы, использующие это хранилище
- Доменные сущности (Task, Decision, Artifact) не меняются
- Агенты не меняются (они зависят от интерфейсов сервисов)


---

## End of Document

Этот документ определяет границы системы Agent Developer и описывает, как реализуются доменные сущности из DOMAIN_ARCHITECTURE.md.

System Boundaries — это мост между доменной моделью (что есть) и реализацией (как работает).

### Ключевые принципы

1. **Services implement Domain operations** — сервисы обеспечивают работу с доменными сущностями
2. **Runtime is replaceable** — runtime может быть заменён без изменения доменной модели
3. **Storage is replaceable** — storage может быть заменён без изменения сервисов
4. **Projections are representations** — проекции это формы представления, не сущности
5. **Agents implement Roles** — агенты реализуют роли из доменной модели
6. **Data flows through layers** — данные движутся от Domain через System Boundaries к Storage
7. **Registry Service is a Facade** — единая точка доступа над тремя специализированными реестрами
8. **Execution Service is decoupled** — принимает Tool объект, не зависит от Registry

### Что описано в этом документе

**Services Layer:**
- Knowledge Service — управление Knowledge Items
- Memory Service — агрегация Task/Project Memory
- Learning Service — извлечение знаний из задач
- Search Service — семантический и полнотекстовый поиск
- Registry Service — фасад над SkillRegistry, ToolRegistry, ReleaseRegistry
- Execution Service — универсальный исполнитель Tool объектов

**Runtime Layer:**
- Runtime Session — контекст выполнения задачи
- Execution Context — состояние исполнения
- Queues — управление очередями задач и файлов
- Caches — кэширование для ускорения доступа

**Agent Implementations:**
- Architect Agent — принимает архитектурные решения
- Planner Agent — создаёт план реализации
- Coder Agent — пишет код и тесты
- Reviewer Agent — ревьюит код
- Integrator Agent — интегрирует код
- Learning Agent — извлекает знания

**Storage Layer:**
- Markdown — текстовые артефакты и документы
- JSON — структурированные данные
- SQLite — сущности с возможностью запросов
- Qdrant — векторное хранилище для семантического поиска
- Git — версионирование документов и кода

**Projection Layer:**
- Document as projection — формы представления доменных сущностей

**Data Flow:**
- Task Execution Flow — полный цикл выполнения задачи
- Tool Execution Flow — выполнение инструментов (демонстрирует decoupling)
- Knowledge Retrieval Flow — поиск знаний
- Memory Aggregation Flow — агрегация памяти

**Service Contracts:**
- Interface Segregation
- Dependency Inversion
- Single Responsibility
- Open/Closed Principle
- Separation of Concerns

### Связь с другими документами

- **DOMAIN_ARCHITECTURE.md** — определяет вечные сущности (что есть)
- **SYSTEM_BOUNDARIES.md** (этот документ) — определяет реализацию (как работает)
- **TASK_LIFECYCLE.md** — определяет поведение (этапы задачи)

### Architecture Law #1

> *See Architecture Law #1 in DOMAIN_ARCHITECTURE.md.*

Этот закон гарантирует, что system boundaries могут эволюционировать независимо от доменной модели.

### Future Evolution

**v2 Planned Changes:**
- Execution Service: переход от `execute(tool: Tool, args)` к `execute(request: ExecutionRequest)` для поддержки sandbox, env, cwd, stdin, timeout, resource limits, telemetry
- Registry Service: may evolve from an in-process facade to independently deployable services while preserving the public contract

