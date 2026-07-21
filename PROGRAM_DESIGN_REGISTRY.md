# PROGRAM_DESIGN_REGISTRY

**Version:** v2.0
**Status:** ACTIVE
**Type:** Registry
**Canonical Source for:** Runtime representation of repository documents for PROGRAM_DESIGN algorithm
**Last Updated:** 2026-07-20

---

# PART I: METADATA AND CONSTRUCTION RULES

## Purpose

PROGRAM_DESIGN_REGISTRY is a **lossless runtime projection** of PROGRAM_DESIGN_PASSPORTS for the PROGRAM_DESIGN algorithm.

Registry contains only information required for deterministic execution of PROGRAM_DESIGN. It discards information not used by the algorithm, but never loses information that the algorithm requires.

Registry is maintained by an engineer and edited manually (e.g., via `nano`), alongside PROGRAM_DESIGN_PASSPORTS. Both documents are first-class engineering artifacts.

---

## Construction Rules

### Rule 1: Source of Truth

PROGRAM_DESIGN_REGISTRY is derived exclusively from PROGRAM_DESIGN_PASSPORTS. No manual inference is permitted.

### Rule 2: Field Extraction

Registry fields are extracted from passports as follows:

**Document Name:**
Primary key of the Registry entry. Extracted from passport filename.

**Canonical Responsibility:**
Extracted from the passport's canonical responsibility description (section "Основная ответственность" or "Определяет"). Used by PROGRAM_DESIGN Phase 2 for semantic matching with Scope Items.

**Structural Dependencies:**
Extracted from the passport dependency model (section "Входящие зависимости"). Used by PROGRAM_DESIGN Phase 4 for forward graph traversal.

**Structural Dependents:**
Deterministically derived by reverse traversal of all passports' Structural Dependencies. Structural Dependents are **not independent registry data** — they are a computed projection. If document A lists document B in its Structural Dependencies, then B lists A in its Structural Dependents. Used by PROGRAM_DESIGN Phase 5 for Review Candidate identification.

### Rule 3: Minimality Invariant

PROGRAM_DESIGN_REGISTRY shall contain **only** fields required by PROGRAM_DESIGN runtime. Any field not used by at least one phase of the algorithm must not appear in Registry.

### Rule 4: Bidirectional Consistency Invariant

For every edge A → B in Structural Dependencies, Registry shall contain the reverse edge B ← A in Structural Dependents. This invariant is mathematically guaranteed by Rule 2 and must hold for all entries.

### Rule 5: Lossless Projection

Registry is a lossless projection relative to PROGRAM_DESIGN requirements. It may discard information not used by the algorithm, but it must preserve all information that the algorithm requires for deterministic execution.

---

## Engineering Invariants

1. **Registry as Derived Artifact:** Registry is derived from PROGRAM_DESIGN_PASSPORTS. Every entry must have a corresponding passport.

2. **Minimal Fields:** Registry contains exactly four fields per document: Document Name, Canonical Responsibility, Structural Dependencies, Structural Dependents.

3. **Bidirectional Consistency:** For every pair (A, B), if A.Structural_Dependencies contains B, then B.Structural_Dependents contains A.

4. **Lossless Projection:** Registry preserves all information required by PROGRAM_DESIGN and discards only information not used by the algorithm.

5. **Registry Synchronization:** Any change to PROGRAM_DESIGN_PASSPORTS that affects Registry fields shall be reflected in PROGRAM_DESIGN_REGISTRY before PROGRAM_DESIGN is executed. Both documents are maintained manually and must remain synchronized.

---

## Registry Schema

For each document in the repository, Registry contains:

**Document Name** (Primary Key)
Unique identifier of the document. Used for cross-referencing.

**canonical_responsibility**
Engineering responsibility of the document. Used by PROGRAM_DESIGN Phase 2 for semantic matching with Scope Items.

**structural_dependencies**
List of documents that this document depends on architecturally. Used by PROGRAM_DESIGN Phase 4 for forward graph traversal.

**structural_dependents**
List of documents that depend on this document architecturally. Derived by reverse traversal of all Structural Dependencies. Used by PROGRAM_DESIGN Phase 5 for Review Candidate identification.

---

# PART II: REGISTRY ENTRIES

## README.md

canonical_responsibility:
  - Назначение репозитория Agent Developer Memory
  - Архитектурные слои документации
  - Перечень основных документов каждого слоя
  - Структуру документации репозитория
  - Текущий этап развития проекта

structural_dependencies: []

structural_dependents: []

---

## PROJECT_GOVERNANCE.md

canonical_responsibility:
  - стратегию проекта
  - высший закон (Supreme Law)
  - видение системы
  - состав продуктов
  - стратегические цели
  - этапы развития
  - принципы разработки
  - процесс управления
  - классификацию изменений
  - архитектурные инварианты
  - критерии принятия решений

structural_dependencies:
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md

structural_dependents:
  - CODE_INDEX.md
  - LAYER3_ROADMAP.md

---

## INFORMATION_ARCHITECTURE.md

canonical_responsibility:
  - структуру инженерной документации
  - уровни (Layers) системы знаний
  - жизненный цикл документов
  - типы документов
  - контракты документов
  - концепцию Canonical Source
  - информационные потоки
  - информационные инварианты
  - роли Authority и Maintainer
  - правила эволюции документации
  - порядок создания документов

structural_dependencies: []

structural_dependents:
  - PROJECT_PROTOCOL.md
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md
  - ENGINEERING_PLAYBOOK.md
  - DOC_STANDARD.md
  - RELEASE_PROCESS.md
  - AUTOMATION.md
  - ENGINEERING_HISTORY.md
  - CURRENT_CONTEXT.md
  - DOCUMENTS.md
  - GLOSSARY.md
  - PROGRAM_MANAGEMENT.md
  - PROGRAMS.md
  - REPOSITORIES.md
  - CODE_INDEX.md

---

## PROJECT_PROTOCOL.md

canonical_responsibility:
  - идентичность проекта
  - миссию и видение
  - область применения
  - роли участников
  - полномочия принятия решений
  - инженерные принципы
  - иерархию Source of Truth
  - правила разрешения конфликтов
  - структуру репозиториев
  - жизненный цикл самого документа

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md

structural_dependents:
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md
  - ENGINEERING_PLAYBOOK.md
  - DOC_STANDARD.md
  - RELEASE_PROCESS.md
  - AUTOMATION.md
  - ENGINEERING_HISTORY.md
  - CURRENT_CONTEXT.md
  - DOCUMENTS.md
  - PROGRAM_MANAGEMENT.md
  - PROGRAMS.md
  - REPOSITORIES.md
  - CODE_INDEX.md

---

## DOMAIN_ARCHITECTURE.md

canonical_responsibility:
  - доменную модель системы
  - состав доменных сущностей
  - контракты сущностей
  - связи между сущностями
  - модели состояний (FSM)
  - модель событий
  - модель ролей
  - архитектурные границы между Domain, Runtime, Services и Storage

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md

structural_dependents:
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md
  - PROJECT_GOVERNANCE.md
  - CODE_INDEX.md
  - LAYER3_ROADMAP.md
  - GLOSSARY.md

---

## SYSTEM_BOUNDARIES.md

canonical_responsibility:
  - сервисный слой системы
  - Runtime
  - реализации ролей через агентов
  - способы хранения данных
  - проекции доменных сущностей
  - потоки данных между слоями
  - контракты сервисов
  - архитектурные границы реализации

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - DOMAIN_ARCHITECTURE.md

structural_dependents:
  - TASK_LIFECYCLE.md
  - PROJECT_GOVERNANCE.md
  - CODE_INDEX.md
  - LAYER3_ROADMAP.md

---

## TASK_LIFECYCLE.md

canonical_responsibility:
  - полный процесс выполнения задачи
  - последовательность Stage 0–12
  - входы и выходы каждого этапа
  - создаваемые артефакты
  - роли агентов
  - Quality Gates
  - переходы между этапами
  - Failure Path
  - обязательные обновления документации

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md

structural_dependents:
  - PROJECT_GOVERNANCE.md
  - CODE_INDEX.md
  - LAYER3_ROADMAP.md

---

## ENGINEERING_PLAYBOOK.md

canonical_responsibility:
  - общий инженерный workflow
  - правила управления изменениями
  - требования к тестированию и верификации
  - инженерные best practices
  - инженерные инварианты
  - правила использования Git
  - правила использования AI в разработке
  - требования к доказательной базе (Evidence)

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md

structural_dependents:
  - DOC_STANDARD.md
  - RELEASE_PROCESS.md
  - AUTOMATION.md
  - ENGINEERING_HISTORY.md
  - PROGRAM_MANAGEMENT.md
  - CODE_INDEX.md

---

## DOC_STANDARD.md

canonical_responsibility:
  - требования к инженерной документации
  - правила оформления документов
  - правила локализации
  - требования к инженерным утверждениям
  - требования к shell-документации
  - требования к heredoc
  - требования к метаданным
  - правила именования
  - правила перекрёстных ссылок
  - критерии качества документации

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - ENGINEERING_PLAYBOOK.md

structural_dependents:
  - RELEASE_PROCESS.md
  - AUTOMATION.md
  - GLOSSARY.md
  - CODE_INDEX.md

---

## RELEASE_PROCESS.md

canonical_responsibility:
  - типы релизов
  - правила Semantic Versioning
  - процесс подготовки релиза
  - требования к верификации перед выпуском
  - чек-лист готовности релиза
  - действия после выпуска
  - процедуру экстренных Hotfix

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - ENGINEERING_PLAYBOOK.md
  - DOC_STANDARD.md

structural_dependents:
  - AUTOMATION.md
  - CODE_INDEX.md

---

## AUTOMATION.md

canonical_responsibility:
  - принципы автоматизации
  - критерии, когда автоматизация необходима
  - реестр существующих автоматизаций
  - правила организации автоматизаций
  - требования к инженерным скриптам
  - процедуру добавления новой автоматизации
  - модель триггеров
  - требования к Verification Automation

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - ENGINEERING_PLAYBOOK.md
  - RELEASE_PROCESS.md

structural_dependents:
  - CODE_INDEX.md

---

## ENGINEERING_HISTORY.md

canonical_responsibility:
  - структуру записей Engineering History
  - обязательные и необязательные поля каждой записи
  - категории инженерного опыта
  - правила написания записей
  - процесс Review и Approval
  - долговременную инженерную память проекта

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - ENGINEERING_PLAYBOOK.md

structural_dependents:
  - CODE_INDEX.md

---

## CURRENT_CONTEXT.md

canonical_responsibility:
  - текущее состояние проекта
  - текущий инженерный фокус
  - статус архитектуры по слоям
  - последние изменения
  - ближайшие шаги разработки

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md

structural_dependents: []

---

## ARCHITECTURE.md

canonical_responsibility:
  - действующие архитектурные соглашения проекта
  - порядок разрешения конфликтов между источниками знаний
  - контракт FileState FSM
  - правила маршрутизации LangGraph
  - правила использования каталога evidence/

structural_dependencies:
  - adr/002-filestate-fsm-v1.3.md
  - adr/003-knowledge-supremacy.md
  - adr/004-pure-router.md
  - adr/005-lean-memory-architecture.md

structural_dependents: []

---

## CODE_INDEX.md

canonical_responsibility:
  - перечень существующих файлов проекта
  - критерии признания файла существующим
  - ссылки на подтверждающие Evidence
  - перечень кандидатов на будущую реализацию
  - назначение каждого зарегистрированного файла

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - PROJECT_GOVERNANCE.md
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md
  - ENGINEERING_PLAYBOOK.md
  - DOC_STANDARD.md
  - RELEASE_PROCESS.md
  - AUTOMATION.md
  - ENGINEERING_HISTORY.md
  - LAYER3_ROADMAP.md

structural_dependents: []

---

## DOCUMENTS.md

canonical_responsibility:
  - полный перечень документов проекта
  - тип каждого документа
  - принадлежность к архитектурному слою
  - жизненный цикл документов
  - статус документов
  - определения типов документов
  - определения архитектурных слоёв
  - значения статусов документации

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md

structural_dependents: []

---

## GLOSSARY.md

canonical_responsibility:
  - единый реестр инженерных терминов
  - категории терминологии
  - краткие идентифицирующие определения
  - Canonical Source каждого термина
  - правила использования терминологии
  - правила регистрации новых терминов
  - требования к согласованности терминологии проекта

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - DOC_STANDARD.md
  - PROGRAM_MANAGEMENT.md
  - DOMAIN_ARCHITECTURE.md

structural_dependents: []

---

## INFRASTRUCTURE.md

canonical_responsibility:
  - аппаратную инфраструктуру
  - программный стек
  - подтверждённые инженерные активы
  - зарегистрированные сервисы
  - только факты, подтверждённые Evidence

structural_dependencies:
    - evidence/

structural_dependents: []

---

## LAYER3_ROADMAP.md

canonical_responsibility:
  - дорожную карту реализации Runtime
  - предварительный состав Runtime-компонентов
  - последовательность итераций реализации
  - Definition of Done для каждой итерации
  - концепцию Vertical Slice
  - зависимости между компонентами
  - стратегию интеграции
  - разделение базового Runtime и Production Features

structural_dependencies:
  - DOMAIN_ARCHITECTURE.md
  - SYSTEM_BOUNDARIES.md
  - TASK_LIFECYCLE.md
  - PROJECT_GOVERNANCE.md

structural_dependents: []

---

## PROGRAM_MANAGEMENT.md

canonical_responsibility:
  - модель инженерных программ
  - терминологию Program Management
  - жизненный цикл программ
  - правила переходов между состояниями
  - правила Frozen Plan
  - управление Backlog
  - правила Review и Retrospective
  - инженерные инварианты управления программами

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - ENGINEERING_PLAYBOOK.md

structural_dependents:
  - PROGRAMS.md
  - GLOSSARY.md
  - adr/008-exclude-portfolio-registry.md

---

## PROGRAMS.md

canonical_responsibility:
  - перечень всех программ проекта
  - статус каждой программы
  - даты начала и завершения
  - цель каждой программы
  - текущий состав инженерного портфеля программ

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md
  - PROGRAM_MANAGEMENT.md

structural_dependents: []

---

## RELEASES.md

canonical_responsibility:
  - перечень выпущенных версий
  - статус каждого релиза
  - инженерные достижения
  - ссылки на подтверждающие Evidence
  - измеренные показатели производительности (при наличии)

structural_dependencies: []

structural_dependents: []

---

## REPOSITORIES.md

canonical_responsibility:
  - перечень репозиториев проекта
  - назначение каждого репозитория
  - URL репозиториев
  - ветки по умолчанию
  - baseline-версии
  - владельцев
  - статус репозиториев
  - общие правила организации репозиториев

structural_dependencies:
  - INFORMATION_ARCHITECTURE.md
  - PROJECT_PROTOCOL.md

structural_dependents: []

---

## adr/INDEX.md

canonical_responsibility:
  - перечень всех ADR проекта
  - идентификатор каждого решения
  - название решения
  - текущий статус решения
  - информацию о замещении (Superseded By)

structural_dependencies: []

structural_dependents: []

---

## adr/000-project-history.md

canonical_responsibility:
  - исходную цель проекта
  - последовательность ранних архитектурных решений
  - первоначальную эволюцию архитектуры
  - границу между историческими решениями и актуальной документацией

structural_dependencies: []

structural_dependents:
  - adr/001-reject-cli-agents.md
  - adr/005-lean-memory-architecture.md

---

## adr/001-reject-cli-agents.md

canonical_responsibility:
  - причину отказа от интерактивных CLI/TUI-агентов
  - выбор LangGraph как основы оркестрации
  - использование явных конечных автоматов состояний (FSM)
  - ожидаемые архитектурные преимущества выбранного подхода

structural_dependencies:
  - adr/000-project-history.md

structural_dependents:
  - adr/002-filestate-fsm-v1.3.md
  - adr/003-knowledge-supremacy.md
  - adr/004-pure-router.md
  - adr/006-tool-layer-strategy.md
  - adr/007-llm-access-strategy.md

---

## adr/002-filestate-fsm-v1.3.md

canonical_responsibility:
  - спецификацию FileState FSM v1.3
  - правила обработки состояний файлов
  - семантику поля retries
  - требования для перехода архитектурного решения в статус ACCEPTED

structural_dependencies:
  - adr/001-reject-cli-agents.md

structural_dependents:
  - ARCHITECTURE.md

---

## adr/003-knowledge-supremacy.md

canonical_responsibility:
  - порядок доверия к источникам знаний
  - правила разрешения конфликтов между источниками
  - роль Memory Layer (Qdrant) в архитектуре
  - требования к будущей реализации данного механизма

structural_dependencies:
  - adr/001-reject-cli-agents.md

structural_dependents:
  - ARCHITECTURE.md

---

## adr/004-pure-router.md

canonical_responsibility:
  - требования к Router-узлам
  - разделение маршрутизации и обработки
  - правила мутации состояния
  - инженерное подтверждение данного решения

structural_dependencies:
  - adr/001-reject-cli-agents.md

structural_dependents:
  - ARCHITECTURE.md
  - adr/006-tool-layer-strategy.md

---

## adr/005-lean-memory-architecture.md

canonical_responsibility:
  - минимальную структуру инженерной памяти
  - состав обязательных документов
  - правила обновления документации
  - принципы снижения стоимости сопровождения

structural_dependencies:
  - adr/000-project-history.md

structural_dependents:
  - ARCHITECTURE.md

---

## adr/006-tool-layer-strategy.md

canonical_responsibility:
  - стратегию организации Tool Layer для Beta-0.1a
  - правила размещения операций записи и валидации
  - критерии появления отдельного модуля tools.py
  - инженерное подтверждение принятого решения

structural_dependencies:
  - adr/001-reject-cli-agents.md
  - adr/004-pure-router.md

structural_dependents: []

---

## adr/007-llm-access-strategy.md

canonical_responsibility:
  - способ взаимодействия с локальными LLM
  - допустимый интерфейс доступа к моделям
  - технические требования к LLM API
  - критерии пересмотра архитектурного решения
  - инженерное подтверждение выбранного подхода

structural_dependencies:
  - adr/001-reject-cli-agents.md
  - adr/006-tool-layer-strategy.md

structural_dependents: []

---

## adr/008-exclude-portfolio-registry.md

canonical_responsibility:
  - изменение состава Program Recovery v1
  - причины исключения Program Portfolio
  - причины исключения отдельного Program Registry
  - влияние решения на дальнейшую структуру документации

structural_dependencies:
  - PROGRAM_MANAGEMENT.md

structural_dependents: []

---

## bootstrap/README.md

canonical_responsibility:
  - назначение Bootstrap
  - состав Bootstrap
  - правило использования Bootstrap
  - направление зависимостей между Bootstrap и Runtime
  - общий процесс создания нового репозитория

structural_dependencies: []

structural_dependents:
  - bootstrap/docs/ARCHITECTURE.md.template
  - bootstrap/docs/DECISIONS.md.template
  - bootstrap/docs/ENGINEERING_RULES.md
  - bootstrap/docs/IMPLEMENTATION_LOG.md.template
  - bootstrap/docs/README.md.template
  - bootstrap/templates/README.md.template
  - bootstrap/templates/.gitignore.template
  - bootstrap/templates/__init__.py.template
  - bootstrap/scripts/bootstrap-layout.sh.template

---

## bootstrap/docs/ARCHITECTURE.md.template

canonical_responsibility:
  - базовую структуру документа Architecture
  - обязательные разделы архитектурного описания
  - места заполнения проектной информацией
  - минимальные требования к архитектурной документации нового репозитория

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/docs/README.md.template

---

## bootstrap/docs/DECISIONS.md.template

canonical_responsibility:
  - структуру документа Architectural Decisions
  - минимальный формат локального ADR
  - обязательные поля архитектурного решения
  - пример оформления первой записи

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/docs/README.md.template

---

## bootstrap/docs/ENGINEERING_RULES.md

canonical_responsibility:
  - фундаментальные инженерные принципы
  - правила построения архитектуры
  - требования к качеству кода
  - обязательные стандарты разработки
  - правила инженерного процесса
  - архитектурные ограничения между слоями системы

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/docs/README.md.template
  - bootstrap/scripts/check.sh.template
  - bootstrap/scripts/smoke.sh.template

---

## bootstrap/docs/IMPLEMENTATION_LOG.md.template

canonical_responsibility:
  - структуру журнала реализации
  - обязательные разделы каждой фазы разработки
  - минимальный набор сведений для документирования инженерного прогресса
  - пример оформления первой записи

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/docs/README.md.template

---

## bootstrap/docs/README.md.template

canonical_responsibility:
  - назначение каталога документации
  - перечень основных инженерных документов
  - правила пополнения документации
  - точку входа для изучения документации нового репозитория

structural_dependencies:
  - bootstrap/README.md
  - bootstrap/docs/ARCHITECTURE.md.template
  - bootstrap/docs/DECISIONS.md.template
  - bootstrap/docs/IMPLEMENTATION_LOG.md.template
  - bootstrap/docs/ENGINEERING_RULES.md

structural_dependents: []

---

## bootstrap/templates/README.md.template

canonical_responsibility:
  - структуру основного README репозитория
  - обязательные разделы пользовательской документации
  - требования к окружению
  - стандартную процедуру установки
  - ссылки на инженерную документацию
  - правила отображения текущего состояния проекта

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/scripts/bootstrap-layout.sh.template

---

## bootstrap/templates/.gitignore.template

canonical_responsibility:
  - перечень файлов, не подлежащих версионированию
  - стандартные категории исключений
  - базовые правила очистки репозитория
  - минимальный набор игнорируемых артефактов разработки

structural_dependencies:
  - bootstrap/README.md

structural_dependents:
  - bootstrap/scripts/bootstrap-layout.sh.template

---

## bootstrap/templates/__init__.py.template

canonical_responsibility:
  - минимальную структуру файла __init__.py
  - наличие документации модуля
  - отсутствие публичного API по умолчанию

structural_dependencies:
  - bootstrap/README.md

structural_dependents: []

---

## bootstrap/scripts/bootstrap-layout.sh.template

canonical_responsibility:
  - создание стандартной структуры репозитория
  - проверку корректности входных параметров
  - проверку наличия Bootstrap-шаблонов
  - копирование базовых файлов
  - последовательность дальнейших действий после создания репозитория

structural_dependencies:
  - bootstrap/README.md
  - bootstrap/templates/README.md.template
  - bootstrap/templates/.gitignore.template

structural_dependents: []

---

## bootstrap/scripts/check.sh.template

canonical_responsibility:
  - последовательность обязательных проверок качества
  - требования к установленным инструментам разработки
  - единый механизм обработки ошибок
  - критерий успешного прохождения полной проверки проекта

structural_dependencies:
  - bootstrap/docs/ENGINEERING_RULES.md

structural_dependents: []

---

## bootstrap/scripts/smoke.sh.template

canonical_responsibility:
  - минимальный набор обязательных проверок после изменения кода
  - критерии успешной базовой работоспособности проекта
  - последовательность выполнения быстрых проверок

structural_dependencies:
  - bootstrap/docs/ENGINEERING_RULES.md

structural_dependents: []

---

## decisions/016-closure.md

canonical_responsibility:
  - итоговый статус каждого незавершённого направления
  - причины принятого решения
  - административное завершение исторического технического долга
  - дальнейшие действия после закрытия списка

structural_dependencies: []

structural_dependents: []

---

## PROGRAM_DESIGN.md

canonical_responsibility:
- Детерминированный алгоритм построения замороженных инженерных программ
- 15-фазный pipeline проектирования программ
- Change Trigger Catalog
- Frozen Program Output Contract
- Program Proof (трассируемость от Scope Items до Completion Criteria)

structural_dependencies:
- PROGRAM_DESIGN_REGISTRY.md

structural_dependents: []

---

## PROGRAM_DESIGN_PASSPORTS.md

canonical_responsibility:
  - Canonical Source инженерных паспортов документов репозитория
  - Правила построения паспортов (Passport Construction Standard)
  - Обязательные разделы паспорта
  - Принципы анализа документов
  - Полная коллекция паспортов всех документов репозитория

structural_dependencies: []

structural_dependents:
  - PROGRAM_DESIGN_REGISTRY.md

---

## PROGRAM_DESIGN_REGISTRY.md

canonical_responsibility:
  - Операционная модель репозитория для алгоритма PROGRAM_DESIGN
  - Lossless runtime projection PROGRAM_DESIGN_PASSPORTS
  - Construction Rules для построения Registry из паспортов
  - Минимальный набор полей для каждого документа
  - Инварианты Registry (Bidirectional Consistency, Minimality, Lossless Projection)
  - Полная коллекция записей для всех документов репозитория

structural_dependencies:
  - PROGRAM_DESIGN_PASSPORTS.md

structural_dependents:
  - PROGRAM_DESIGN.md

---

## END OF REGISTRY
