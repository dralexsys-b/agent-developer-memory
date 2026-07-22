# PROGRAM_DESIGN

**Version:** 2.2
**Status:** FROZEN
**Type:** Standard / Algorithm
**Canonical Source for:** Процесс проектирования безопасных инженерных программ, обеспечивающих сохранение согласованности Engineering Knowledge Repository.

---

## Purpose

PROGRAM_DESIGN определяет детерминированный алгоритм построения замороженных инженерных программ (Frozen Programs), обеспечивающих сохранение согласованности репозитория.

Это не рекомендация. Это **исполняемый алгоритм для LLM**.

Результатом работы алгоритма является не просто список коммитов, а полноценный инженерный контракт: последовательность изменений вместе с доказательством того, что после их выполнения репозиторий останется согласованным и достигнет всех заявленных целей.

---

## Registry Origin

PROGRAM_DESIGN_PASSPORTS is the Canonical Source for PROGRAM_DESIGN_REGISTRY.
PROGRAM_DESIGN_REGISTRY является runtime representation паспортов и содержит только сведения, необходимые для исполнения этого алгоритма.
Access to PROGRAM_DESIGN_PASSPORTS is outside the scope of this algorithm.

---

## Execution Baseline

Execution Baseline — это фиксированный и полный набор входных данных, существующий **до** начала исполнения алгоритма. Он определяет воспроизводимость исполнения программы.

**Baseline ID:** implementation-defined, must be unique
**Baseline Created At:** YYYY-MM-DD HH:MM:SS UTC
**Inputs:**
- PROGRAM_DESIGN version
- PROGRAM_DESIGN_REGISTRY version
- Program Definition
- Repository Snapshot (обязательно как идентификатор: Git Commit Hash, Snapshot ID или Archive ID)

**Invariant:** Execution Baseline существует до начала исполнения алгоритма и не является частью алгоритма. Любая модификация Baseline делает текущее исполнение недействительным и требует генерации **новой программы с собственным Program ID и собственной Revision 0**.

---

## Engineering Invariants

1. **Minimal Context Principle:** PROGRAM_DESIGN требует только данные из Execution Baseline для работы.

2. **Registry as Sole Source:** PROGRAM_DESIGN использует PROGRAM_DESIGN_REGISTRY из Execution Baseline как единственный источник информации о документах репозитория. Алгоритм не имеет права предполагать существование или содержание каких-либо других документов.

3. **Absence of Ambiguity Resolution:** PROGRAM_DESIGN никогда не выбирает один документ из нескольких валидных совпадений. Все документы, чья Canonical Responsibility matches the Scope Item, включаются.

4. **Metadata Requirements, Not Actions:** PROGRAM_DESIGN не изменяет паспорта или Registry напрямую. Алгоритм определяет требования к обновлению метаданных, которые включаются во Frozen Program.

5. **Self-Extension:** PROGRAM_DESIGN, PROGRAM_DESIGN_REGISTRY и PROGRAM_DESIGN_PASSPORTS являются обычными элементами системы и подчиняются тем же правилам.

6. **Repository Consistency:** После выполнения любой программы репозиторий обязан оставаться полностью согласованным, включая его метаданные.

7. **Traceability:** Каждый Scope Item обязан быть трассируемым до хотя бы одного Completion Criterion через цепочку Change Record → Commit → Validation.

8. **Baseline Immutability:** Execution Baseline остаётся неизменным в течение всего исполнения программы. Любое изменение Baseline требует создания новой программы с новым Baseline ID, новым Program ID и собственной Revision 0.

---

## Preconditions

Pipeline может быть запущен только при выполнении следующих условий:
- Execution Baseline установлен и задокументирован.

Если Execution Baseline не установлен, Pipeline не может быть запущен.

---

# PART I: PROGRAM DESIGN PIPELINE

## PHASE 1: Program Definition Validation

**Вход:** Program Definition (from Execution Baseline)

**Задача:** Извлечь и проверить наличие обязательных полей определения программы.

**Выход:**
- Program Name
- Purpose
- Scope (нумерованный список; каждый элемент списка далее называется **Scope Item**)
- Out of Scope
- Completion Criteria (нумерованный список)

**Validation:** Все пять полей заполнены и не противоречат друг другу.

---

## PHASE 2: Repository Entry Discovery

**Вход:** Scope (из Phase 1)

**Задача:** Найти документы, чья Canonical Responsibility matches the Scope Items.

**Правило:** Для каждого Scope Item найти в PROGRAM_DESIGN_REGISTRY документы, чья Canonical Responsibility matches the Scope Item.

**Выход:** Entry Documents (список документов с обоснованием сопоставления).

**Validation:** Для каждого Entry Document указано, какой Scope Item он покрывает.

---

## PHASE 3: Missing Responsibilities Detection

**Вход:** Scope (из Phase 1), Entry Documents (из Phase 2)

**Задача:** Обнаружить Scope Items, для которых не найдено ни одного Entry Document.

**Правило:** Если Scope Item не имеет Entry Document (ни один документ в Registry не имеет Canonical Responsibility, которая matches the Scope Item), создать New Document Proposal.

**Выход:**
- Covered Scope Items
- New Document Proposals (с Canonical Responsibility, Proposed Document Type и Reason)

**Validation:** Каждый Scope Item либо имеет Entry Document, либо имеет New Document Proposal.

---

## PHASE 4: Dependency Closure

**Вход:** Entry Documents (из Phase 2)

**Задача:** Построить транзитивное замыкание зависимостей.

**Expansion Rules:**

**Rule 1: Structural Dependencies (forward only)**
Для каждого Entry Document добавить все документы из поля Structural Dependencies.

**Rule 2: Repeat until stable**
Повторять Rule 1, пока Dependency Closure не перестанет изменяться.

**Выход:** Dependency Closure (Entry Documents + все транзитивные зависимости).

**Validation:** Dependency Closure не содержит дубликатов.

---

## PHASE 5: Classification

**Вход:** Dependency Closure (из Phase 4), Scope (из Phase 1), PROGRAM_DESIGN_REGISTRY

**Задача:** Классифицировать документы и явно выявить кандидатов на проверку.

**Алгоритм:**
1. **Required Change:** Документы из Dependency Closure, чья Canonical Responsibility matches хотя бы одному Scope Item.
2. **Review Candidate:** Для каждого документа из Required Change получить его Structural Dependents из PROGRAM_DESIGN_REGISTRY. Если такой dependent документ ещё не классифицирован как Required Change, он становится Review Candidate.
3. **No Change:** Все остальные документы из Dependency Closure.

**Выход:**
- Documents To Change (Required Change с обоснованием)
- Review Candidates (Review Candidate с обоснованием)
- Unchanged Documents (No Change с обоснованием)

**Validation:** Каждый документ из Unchanged имеет явное объяснение, почему программа его не затрагивает.

---

## PHASE 6: Change Records Formation

**Вход:** Documents To Change (из Phase 5), Review Candidates (из Phase 5), New Document Proposals (из Phase 3)

**Задача:** Сформировать Change Record для каждого документа, требующего действия.

**Выход:** Change Records, каждая содержит:
- Document (имя файла или "NEW: [Proposed Document Type]" для Proposal)
- Origin (ссылка на Scope Item или Completion Criteria)
- Expected Changes (что должно получиться; для Review Candidate: "Verify consistency and update if necessary")
- Validation Criteria (наблюдаемые условия, подтверждающие успешное завершение, выводятся из Expected Changes)

**Validation:** Каждая запись содержит все четыре поля. Validation Criteria логически следуют из Expected Changes.

---

## PHASE 7: Trigger Classification

**Вход:** Change Records (из Phase 6)

**Задача:** Определить причину изменения, выбрав строгий термин из Part III.

**Выход:** Change Triggers (список пар: Change Record → Trigger).

**Validation:** Каждый триггер существует в каталоге Part III. Придумывать новые триггеры запрещено.

---

## PHASE 8: Work Package Assembly

**Вход:** Change Records + Change Triggers

**Задача:** Сгруппировать изменения в логические блоки работ. Review Candidates must be assigned to dedicated verification work packages.

**Выход:** Work Packages (Name, Goal, Change Records, Dependencies).

**Validation:** Каждый Work Package имеет единую цель. Все Change Records распределены.

---

## PHASE 9: Execution Order

**Вход:** Work Packages (из Phase 8)

**Задача:** Построить граф зависимостей Work Packages, проверить на ацикличность, определить топологический порядок.

**Выход:** Execution Order (топологически упорядоченный список с обоснованием).

**Validation:** Граф проверен на отсутствие циклов. Порядок не нарушает зависимости.

---

## PHASE 10: Commit Planning

**Вход:** Execution Order (из Phase 9)

**Задача:** Превратить Work Packages в последовательность коммитов.

**Выход:** Commit Plan (Commit Message, Files To Change, Goal, Validation).

**Validation:** Формат сообщения соответствует Conventional Commits. Коммиты не нарушают целостность репозитория.

---

## PHASE 11: Frozen Plan Validation

**Вход:** Commit Plan + Program Definition

**Задача:** Проверить полноту покрытия и согласованность плана.

**Validation:**
- [ ] Все документы из Dependency Closure учтены в Commit Plan, Review Candidates или Unchanged.
- [ ] Для каждого изменения указан валидный триггер из Part III.
- [ ] Все документы с категорией Required Change присутствуют в Commit Plan.
- [ ] Все New Document Proposals присутствуют в Commit Plan.
- [ ] **No unexplained changes:** каждый изменяемый документ имеет Trigger, Origin и Expected Changes.
- [ ] **Bidirectional traceability:** каждый Scope Item приводит хотя бы к одному Change Record или New Document Proposal.

**Выход:** Validation Checklist, Validated Plan.

---

## PHASE 12: Repository Metadata Requirements

**Вход:** Validated Plan (из Phase 11)

**Задача:** Определить обязательные требования по поддержанию инженерных метаданных после выполнения программы и добавить их в Validated Plan.

**Правило:** PROGRAM_DESIGN не изменяет паспорта или Registry напрямую. Алгоритм определяет требования, которые включаются в план.

**Выход:** Updated Validated Plan (Validated Plan + Metadata Requirements).

Каждое требование содержит:
- Target (PROGRAM_DESIGN_PASSPORTS или PROGRAM_DESIGN_REGISTRY)
- Requirement Type (Passport Creation Required, Passport Update Required, Registry Synchronization Required)
- Reason (обоснование)
- Affected Documents (список документов)

**Validation:**
- Для каждого New Document Proposal существует требование Passport Creation Required.
- Для каждого изменённого документа существует требование Passport Update Required, если изменение требует актуализации инженерного паспорта документа.
- Для каждого изменения структуры репозитория существует требование Registry Synchronization Required.

---

## PHASE 13: Freeze

**Вход:** Updated Validated Plan (из Phase 12)

**Задача:** Принять инженерное решение о заморозке плана.

**Authority:** Project Architect (требует человеческого подтверждения).

**Выход:** Approved Frozen Program.

**Validation:** Все проверки из Phase 11 пройдены успешно. Подтверждено Project Architect.

---

# PART II: ENGINEERING REVISION AND PUBLICATION

## Engineering Revision

Engineering Revision — это версия инженерного содержания Frozen Program.

**Revision 0** — первая полностью сгенерированная версия Frozen Program на основе Execution Baseline.

**Revision 1, 2, ...** — создаётся только при:
- Обнаружении ошибки в предыдущей ревизии
- Изменении инженерного решения

**Invariants:**
- Engineering Revision preserves Program ID. Все ревизии одной программы имеют одинаковый Program ID, но различаются по номеру ревизии.
- Revision N supersedes Revision N-1. Only the latest Engineering Revision is authoritative.

**Важно:** Изменение Execution Baseline (включая Program Definition, Registry, Repository State) **не создаёт новую ревизию**. Оно порождает **новую программу с собственным Program ID и собственной Revision 0**.

---

## Publication Segments

Publication Segment — это физическое разбиение документа для публикации.

Если Frozen Program не помещается в один носитель (сообщение, PDF, файл), она публикуется как:

Frozen Program Revision 0
- Segment 1
- Segment 2
- Segment 3

или

Frozen Program Revision 0
- Volume I
- Volume II

**Invariants:**
- Segments may be published independently but collectively constitute one Frozen Program.
- Publication order is normative. Segments must be consumed in sequential order.
- Publication Segments не изменяют инженерное содержание программы. Они являются только способом доставки.

---

## Revision vs Publication vs Baseline

| Понятие | Что означает | Когда создаётся |
|---------|--------------|-----------------|
| **Execution Baseline** | Фиксированные входные данные | До начала исполнения алгоритма |
| **Engineering Revision** | Изменение инженерного содержания | При ошибке или изменении решения |
| **Publication Segment** | Физическое разбиение документа | При превышении лимитов носителя |

---

# PART III: CHANGE TRIGGER CATALOG

Все триггеры оформлены как **события**:
- `Program Created` — новая программа добавлена в реестр
- `Program Frozen` — план программы заморожен и утверждён Project Architect
- `Program Completed` — программа завершена
- `Program Archived` — программа архивирована
- `Canonical Source Updated` — изменён документ-источник
- `Dependency Added` — добавлена зависимость
- `Dependency Removed` — удалена зависимость
- `Terminology Changed` — изменена терминология
- `Metadata Changed` — изменены метаданные документа
- `Registry Entry Added` — добавлена запись в реестр
- `Registry Entry Updated` — обновлена запись в реестре
- `Retrospective Added` — добавлена ретроспектива
- `Post-Mortem Added` — добавлен пост-мортем

---

# PART IV: FROZEN PROGRAM OUTPUT CONTRACT

The Frozen Program must contain the following logical sections in the specified order. Rendering format (Markdown, JSON, etc.) is implementation-defined unless otherwise required.

**Required Sections:**

1. **Program Identity**
   - Program ID
   - Engineering Revision
   - Program Generated At
   - Execution Baseline Fingerprint (краткая сводка Baseline: Baseline ID, версии PROGRAM_DESIGN и PROGRAM_DESIGN_REGISTRY, идентификатор Repository Snapshot)

2. Program Definition

3. Repository Entry Discovery Report

4. Missing Responsibilities Detection Report

5. Dependency Closure Report

6. Classification Report (Documents To Change, Review Candidates, Unchanged Documents)

7. Change Records

8. Change Triggers

9. Work Packages

10. Execution Order (Dependency Graph + Topological Order)

11. Commit Plan

12. Validation Checklist

13. Repository Metadata Requirements

14. Freeze Approval

---

## END OF DOCUMENT
