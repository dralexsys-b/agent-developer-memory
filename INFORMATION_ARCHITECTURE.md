# Information Architecture (Информационная архитектура)

**Status:** ACCEPTED
**Version:** 1.0
**Date:** 2026-06-18
**Authority:** Project Architect
**Maintainer:** Project Maintainer

Этот документ определяет информационную архитектуру проекта Agent Developer.
Он стоит НАД системой ADR и сам не является ADR.
Он определяет структуру, в которой существует вся остальная документация.

---

## Scope (Область применения)

Этот документ определяет:
- Как организованы знания проекта
- Какие документы существуют и почему
- Как информация передаётся между слоями
- Какие инварианты должны сохраняться
- Кто имеет Authority и кто поддерживает что

Этот документ НЕ определяет:
- архитектуру Runtime
- Архитектуру программного обеспечения
- Детали реализации
- Инженерные процедуры
- Конкретные ADR

---

## Dependencies (Зависимости)

**Dependencies:** None
**Dependents:** All documentation

Этот документ является абсолютным корнем дерева знаний.
Он не имеет внешних зависимостей.
Все остальные документы зависят от него.

---

## Document Lifecycle Rules (Правила жизненного цикла документа)

Этот документ может только:
- Уточняться
- Расширяться
- Помечаться как DEPRECATED
- Дополняться через appendix

Этот документ НЕ может:
- Полностью переписываться

Если требуется фундаментальное изменение информационной архитектуры,
создайте `INFORMATION_ARCHITECTURE_V2.md` и архивируйте эту версию.


## Information Model (Информационная модель)

Знания проекта организованы в пять слоёв:

### Layer 0: Meta Architecture (Слой 0: Мета-архитектура)

**Purpose:** Описывает саму систему знаний.
**Documents:** INFORMATION_ARCHITECTURE.md
**Question answered:** "Как организованы знания?"
**Lifecycle:** Static
**Update frequency:** Крайне редко (только при необходимости фундаментальной реструктуризации)

---

### Layer 1: Project Identity (Слой 1: Идентичность проекта)

**Purpose:** Определяет идентичность проекта, роли, принципы и структуру.
**Documents:** PROJECT_PROTOCOL.md
**Question answered:** "Что это за проект?"
**Lifecycle:** Static
**Update frequency:** Редко (только при изменении ролей, принципов или структуры)

---

### Layer 2: Operational Knowledge (Слой 2: Операционные знания)

**Purpose:** Описывает текущее операционное состояние проекта.
**Documents:**
- CURRENT_CONTEXT.md (Планируемый документ)
- CODE_INDEX.md (Существует)
- RELEASES.md (Существует)
- ADR_INDEX.md (Планируемый документ)
- DOCUMENTS.md (Планируемый документ)
- REPOSITORIES.md (Планируемый документ)

**Question answered:** "Каково текущее состояние проекта?"
**Lifecycle:** Dynamic
**Update frequency:** Постоянно (изменяется с каждым milestone, релизом или добавлением файла)

---

### Layer 3: Engineering Knowledge (Слой 3: Инженерные знания)

**Purpose:** Определяет, как проект разрабатывается, выпускается и поддерживается.
**Documents:**
- ENGINEERING_PLAYBOOK.md (Планируемый документ)
- DOC_STANDARD.md (Планируемый документ)
- RELEASE_PROCESS.md (Планируемый документ)
- AUTOMATION.md (Планируемый документ)
- ENGINEERING_HISTORY.md (Планируемый документ)

**Question answered:** "Как мы разрабатываем этот проект?"
**Lifecycle:** Semi-static
**Update frequency:** Периодически (изменяется при эволюции процессов)

---

### Layer 4: Verification Layer (Слой 4: Слой верификации)

**Purpose:** Содержит неизменяемые артефакты, подтверждающие состояние, поведение, качество, производительность или воспроизводимость проекта.
**Documents:**
- evidence/ (Существует)
- logs/ (Будущий каталог)
- benchmarks/ (Будущий каталог)
- reports/ (Будущий каталог)

**Question answered:** "Какие у нас есть доказательства?"
**Lifecycle:** Immutable
**Update frequency:** Создаются один раз, никогда не изменяются


## Knowledge Lifecycle (Жизненный цикл знаний)

Каждый документ принадлежит к одной из четырёх категорий жизненного цикла:

### Static (Статический)

**Definition:** Документы, которые почти никогда не изменяются.
**Characteristics:**
- Определяют фундаментальные принципы и структуры
- Изменения требуют архитектурного рецензирования
- Служат стабильной основой для других документов

**Examples:**
- PROJECT_PROTOCOL.md
- ENGINEERING_PLAYBOOK.md
- DOC_STANDARD.md

---

### Semi-static (Полустатический)

**Definition:** Документы, которые изменяются периодически.
**Characteristics:**
- Определяют процессы и процедуры
- Изменения происходят при эволюции процессов
- Обновления планируются и документируются

**Examples:**
- RELEASE_PROCESS.md
- AUTOMATION.md

---

### Dynamic (Динамический)

**Definition:** Документы, которые изменяются постоянно.
**Characteristics:**
- Отражают текущее операционное состояние
- Обновляются часто по мере развития проекта
- Представляют "живые" знания

**Examples:**
- CURRENT_CONTEXT.md
- RELEASES.md
- ENGINEERING_HISTORY.md
- CODE_INDEX.md

---

### Immutable (Неизменяемый)

**Definition:** Артефакты, созданные один раз и никогда не изменяемые.
**Characteristics:**
- Служат историческим свидетельством
- Не могут быть отредактированы после создания
- Если требуется исправление, создаётся новый артефакт с пояснением

**Examples:**
- evidence/ (логи, benchmarks, отчёты)
- ADR файлы (изменения через новый ADR или обновление статуса)


## Document Types (Типы документов)

Каждый документ в проекте принадлежит к одному из следующих типов:

| Type (Тип) | Purpose (Назначение) | Example (Пример) |
|---|---|---|
| **Protocol** | Определяет правила взаимодействия и ответственности | PROJECT_PROTOCOL.md |
| **Standard** | Определяет требования к артефактам | DOC_STANDARD.md |
| **Playbook** | Определяет последовательность действий | ENGINEERING_PLAYBOOK.md |
| **Architecture** | Определяет структуру системы | INFORMATION_ARCHITECTURE.md |
| **Index** | Помогает находить информацию (навигация) | ADR_INDEX.md, DOCUMENTS.md |
| **Registry** | Определяет авторитетный инвентарь сущностей проекта | REPOSITORIES.md, CODE_INDEX.md |
| **History** | Записывает прошлые события | ENGINEERING_HISTORY.md |
| **Context** | Описывает текущее состояние | CURRENT_CONTEXT.md |

### Distinction: Index vs Registry (Различие между Index и Registry)

**Index** помогает находить информацию. Отвечает на вопрос "Где я могу найти X?"
**Registry** — это авторитетный инвентарь. Отвечает на вопрос "Какие сущности существуют?"

Пример:
- DOCUMENTS.md — это **Index** (помогает находить документы)
- REPOSITORIES.md — это **Registry** (официальный список репозиториев)
- CODE_INDEX.md — это **Registry** (официальный список файлов кода)

При создании нового документа сначала определите его тип, затем назначьте имя.

---

## Document Contracts (Контракты документов)

Каждый документ должен иметь контракт, который определяет:

1. **Primary Question:** На какой единственный вопрос отвечает этот документ?
2. **Purpose:** Почему этот документ существует?
3. **Canonical Source:** Какими фактами владеет этот документ?
4. **Dependencies:** На какие другие документы он ссылается?
5. **Dependents:** Какие документы ссылаются на него?
6. **Lifecycle:** Static / Semi-static / Dynamic / Immutable

### Canonical Source Concept (Концепция Canonical Source)

**Definition:** Уникальный документ, владеющий конкретным фактом.

**Rule:** Каждый факт имеет ровно один Canonical Source.

**Example:**
- Текущий milestone → Canonical Source: CURRENT_CONTEXT.md
- Список файлов → Canonical Source: CODE_INDEX.md
- История релизов → Canonical Source: RELEASES.md
- Инженерные принципы → Canonical Source: PROJECT_PROTOCOL.md

Другие документы могут **ссылаться** на эти факты, но никогда не **дублировать** их.


## Information Flows (Потоки информации)

Информация передаётся через систему по определённым паттернам. Эти потоки не являются зависимостями между документами, а скорее представляют движение знаний от создания к потреблению.

### Primary Pipeline (Основной конвейер)

Основной поток информации следует по этому пути:

    Реализация
        ↓
    Evidence (Layer 4)
        ↓
    Валидация
        ↓
    Операционное состояние (Layer 2)
        ↓
    Инженер использует знания

**Description:**
1. Разработчик вносит изменения (Layer 3: Engineering Knowledge)
2. Генерируется Evidence (Layer 4: Verification Layer)
3. Evidence проверяется на соответствие критериям приёмки
4. Обновляется операционное состояние (Layer 2: Operational Knowledge)
5. Инженер читает текущее состояние для понимания проекта

---

### Parallel Flows (Параллельные потоки)

Множественные потоки информации оперируют одновременно:

#### Architecture Decision Flow (Поток архитектурных решений)

    Архитектурное решение
        ↓
    ADR-* (создан)
        ↓
    ADR_INDEX (обновлён)
        ↓
    Инженер ссылается на решение

#### Engineering Process Flow (Поток инженерного процесса)

    Инженерные знания
        ↓
    ENGINEERING_PLAYBOOK
        ↓
    Разработчик следует процедурам

#### Release Process Flow (Поток процесса релиза)

    Процесс релиза
        ↓
    RELEASE_PROCESS
        ↓
    Release Manager выполняет релиз

#### Historical Knowledge Flow (Поток исторических знаний)

    Извлечённые уроки
        ↓
    ENGINEERING_HISTORY
        ↓
    Инженер изучает прошлые решения

---

### Flow Direction Rule (Правило направления потока)

**Authority flows downward.**
**Information may flow upward only as evidence.**

- Layer 0 (Meta Architecture) определяет правила для всех нижних слоёв
- Layer 1 (Project Identity) определяет правила для слоёв 2-4
- Layer 2 (Operational Knowledge) отражает текущее состояние
- Layer 3 (Engineering Knowledge) определяет процедуры
- Layer 4 (Verification Layer) предоставляет evidence

Нижние слои не могут переопределять концепции высших слоёв. Они могут только предоставлять evidence, которое может информировать решения высших слоёв.


## Information Invariants (Информационные инварианты)

Следующие 12 инвариантов должны сохраняться всегда. Нарушение любого инварианта указывает на архитектурную ошибку, которая должна быть исправлена перед продолжением работы.

### Invariant 1: Single Canonical Source (Инвариант 1: Единственный Canonical Source)

Каждый факт имеет ровно один Canonical Source.
Ни один документ не может дублировать факты, принадлежащие другому документу.

### Invariant 2: No Duplication (Инвариант 2: Отсутствие дублирования)

Документы никогда не дублируют факты.
Они могут ссылаться на факты, но никогда не копировать их.

### Invariant 3: Evidence Immutability (Инвариант 3: Неизменяемость Evidence)

Evidence никогда не редактируется после создания.
Если требуется исправление, создаётся новое evidence с пояснением.

### Invariant 4: ADR Immutability (Инвариант 4: Неизменяемость ADR)

ADR файлы никогда не переписываются.
Изменения вносятся через новый ADR или обновление статуса (PROPOSED → ACCEPTED → SUPERSEDED).

### Invariant 5: Current Context Reflects Only Current State (Инвариант 5: CURRENT_CONTEXT отражает только текущее состояние)

CURRENT_CONTEXT отражает только текущее операционное состояние.
Он не содержит исторической информации или процедур.

### Invariant 6: Project Protocol Independence (Инвариант 6: Независимость PROJECT_PROTOCOL)

PROJECT_PROTOCOL не зависит от текущего состояния проекта.
Он определяет идентичность, а не статус.

### Invariant 7: Engineering Procedures in Engineering Documents (Инвариант 7: Инженерные процедуры в инженерных документах)

Все инженерные процедуры находятся только в документах Engineering Knowledge (Layer 3).
Они не появляются в Project Identity или Operational Knowledge.

### Invariant 8: Procedures Are Not Source of Truth (Инвариант 8: Процедуры не являются источником истины)

Процедуры никогда не являются источником истины.
Источник истины — только Core документы (слои 1-2) и Evidence (слой 4).

### Invariant 9: Authority and Maintainer Separation (Инвариант 9: Разделение Authority и Maintainer)

Каждый документ имеет Authority (кто определяет содержимое) и Maintainer (кто обновляет его).
Это роли, а не люди. Один участник может занимать несколько ролей.

### Invariant 10: Single Document Change (Инвариант 10: Изменение одного документа)

Изменение документа не должно требовать изменения нескольких независимых документов.
Если это происходит, архитектура имеет проблему дублирования.

### Invariant 11: One Primary Question (Инвариант 11: Один Primary Question)

Каждый документ должен отвечать на один primary question.
Это предотвращает scope creep и обеспечивает фокус.

### Invariant 12: Authority Flows Downward (Инвариант 12: Authority передаётся вниз)

Authority передаётся вниз.
Информация может передаваться вверх только как evidence.

Нижние слои не могут переопределять концепции высших слоёв.
Они могут только предоставлять evidence, которое может информировать решения высших слоёв.

Пример:
- ENGINEERING_PLAYBOOK (Layer 3) не может изменить PROJECT_PROTOCOL (Layer 1)
- ENGINEERING_PLAYBOOK может только ссылаться на PROJECT_PROTOCOL
- Если требуется изменение, оно должно быть выполнено Authority слоя Layer 1


## Authority & Maintainer (Authority и Maintainer)

Каждый документ имеет две различные роли:

**Authority:** Роль, определяющая содержимое и структуру документа.
**Maintainer:** Роль, выполняющая обновления и исправления.

**Important:** Authority и Maintainer обозначают проектные роли, а не конкретных людей. Один участник может занимать несколько ролей, и роль может быть передана другому участнику без изменения архитектуры документации.

### Role Assignments (Назначения ролей)

| Document (Документ) | Authority | Maintainer |
|---|---|---|
| PROJECT_PROTOCOL.md | Project Architect | Project Maintainer |
| CURRENT_CONTEXT.md | Project Architect | Project Maintainer |
| CODE_INDEX.md | Repository Maintainer | Repository Maintainer |
| RELEASES.md | Release Manager | Release Manager |
| ADR_INDEX.md | Project Architect | Project Maintainer |
| DOCUMENTS.md | Documentation Lead | Documentation Maintainer |
| REPOSITORIES.md | Infrastructure Lead | Infrastructure Maintainer |
| ENGINEERING_PLAYBOOK.md | Engineering Lead | Engineering Maintainer |
| DOC_STANDARD.md | Documentation Lead | Documentation Maintainer |
| RELEASE_PROCESS.md | Release Manager | Release Maintainer |
| AUTOMATION.md | Engineering Lead | Engineering Maintainer |
| ENGINEERING_HISTORY.md | Engineering Lead | Engineering Maintainer |
| evidence/ | QA / Verification | Verification System |

---

## Evolution (Эволюция)

Документы могут эволюционировать в течение своего жизненного цикла. Следующие операции разрешены:

### Permitted Operations (Разрешённые операции)

**Create:** Новый документ добавляется в систему.
**Update:** Существующий документ модифицируется в пределах своей области применения.
**Archive:** Документ помечается как ARCHIVED, но сохраняется для исторической справки.
**Replace:** Документ заменяется новым документом с другим именем.
**Split:** Документ разделяется на несколько документов, когда он выходит за пределы своей области применения.
**Merge:** Несколько документов объединяются, когда их области применения перекрываются.

### Prohibited Operations (Запрещённые операции)

**Rename:** Документ никогда не переименовывается.
Переименование нарушает ссылки и нарушает принцип единственного Canonical Source.

Если документу нужно новое имя:
1. Архивируйте старый документ
2. Создайте новый документ с новым именем
3. Обновите все ссылки

### Version Control (Контроль версий)

Документы отслеживаются через git.
Крупные структурные изменения требуют новой версии (например, INFORMATION_ARCHITECTURE_V2.md).
Незначительные обновления отслеживаются через историю git.


## Compactness Principle (Принцип компактности)

Каждый документ должен оставаться читаемым и иметь единую согласованную тему.

**Rule:** Если в документе появляются несколько независимых тем, они должны быть извлечены в отдельные документы.

Этот принцип обеспечивает, что документы не растут бесконтрольно и остаются сфокусированными на своём primary question.

---

## Creation Order (Порядок создания)

Документы создаются в определённом порядке, чтобы гарантировать, что каждый документ имеет готовый контракт из Information Architecture до его создания:

    INFORMATION_ARCHITECTURE (Layer 0: Meta Architecture)
        ↓
    PROJECT_PROTOCOL (Layer 1: Project Identity)
        ↓
    DOCUMENTS (Layer 2: Operational Knowledge)
        ↓
    REPOSITORIES (Layer 2: Operational Knowledge)
        ↓
    ENGINEERING_PLAYBOOK (Layer 3: Engineering Knowledge)
        ↓
    DOC_STANDARD (Layer 3: Engineering Knowledge)
        ↓
    RELEASE_PROCESS (Layer 3: Engineering Knowledge)
        ↓
    AUTOMATION (Layer 3: Engineering Knowledge)

Каждый последующий документ создаётся с предопределённым контрактом из этой Information Architecture.

---

## Future Evolution (Будущая эволюция)

Ожидается, что информационная архитектура будет эволюционировать путём:

- Введения новых типов документов
- Введения новых Registry (например, SKILL_REGISTRY, MODEL_REGISTRY)
- Введения генерируемой документации
- Введения документации, поддерживаемой агентами
- Автоматизации обновлений Registry из анализа кода

Вся эволюция должна сохранять 12 Information Invariants.

Архитектура разработана для обеспечения роста без фундаментальной реструктуризации. Новые документы должны вписываться в существующую модель слоёв и категории жизненного цикла.

---

## End of Document (Конец документа)

Этот документ определяет информационную архитектуру проекта Agent Developer.
Это фундамент, на котором строится вся остальная документация.
Все остальные документы должны соответствовать принципам и инвариантам, определённым здесь.
