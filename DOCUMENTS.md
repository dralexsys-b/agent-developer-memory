# Documents Registry (Реестр документов)

**Status:** ACTIVE
**Version:** 1.0
**Date:** 2026-06-18
**Authority:** Documentation Lead
**Maintainer:** Documentation Maintainer

**Type:** Index (Layer 2: Operational Knowledge)
**Primary Question:** "What documents exist?"
**Canonical Source for:** Complete registry of project documents
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md
**Dependents:** All project documentation

---

## Registry (Реестр)

| Document (Документ)           | Type (Тип)    | Layer (Слой)       | Lifecycle (Жизненный цикл)  | Status (Статус) |
|-------------------------------|---------------|--------------------|-----------------------------|-----------------|
| `INFORMATION_ARCHITECTURE.md` | Architecture  | 0 (Meta)           | Static                      | ACTIVE          |
| `PROJECT_PROTOCOL.md`         | Protocol      | 1 (Identity)       | Static                      | ACTIVE          |
| `DOCUMENTS.md`                | Index         | 2 (Operational)    | Dynamic                     | ACTIVE          |
| `REPOSITORIES.md`             | Registry      | 2 (Operational)    | Semi-static                 | PLANNED         |
| `CURRENT_CONTEXT.md`          | Context       | 2 (Operational)    | Dynamic                     | ACTIVE          |
| `CODE_INDEX.md`               | Registry      | 2 (Operational)    | Dynamic                     | ACTIVE          |
| `RELEASES.md`                 | History       | 2 (Operational)    | Dynamic                     | ACTIVE          |
| `ADR_INDEX.md`                | Index         | 2 (Operational)    | Dynamic                     | PLANNED         |
| `ENGINEERING_PLAYBOOK.md`     | Playbook      | 3 (Engineering)    | Semi-static                 | PLANNED         |
| `DOC_STANDARD.md`             | Standard      | 3 (Engineering)    | Static                      | PLANNED         |
| `RELEASE_PROCESS.md`          | Playbook      | 3 (Engineering)    | Semi-static                 | PLANNED         |
| `AUTOMATION.md`               | Playbook      | 3 (Engineering)    | Semi-static                 | PLANNED         |
| `ENGINEERING_HISTORY.md`      | History       | 3 (Engineering)    | Dynamic                     | PLANNED         |

---

## Relationships (Связи)

**Dependencies (Зависимости):**
- INFORMATION_ARCHITECTURE.md
- PROJECT_PROTOCOL.md

**Dependents (Зависимые документы):**
- Вся документация проекта

---

## Document Type Definitions (Определения типов документов)

- **Protocol (Протокол)** — определяет правила взаимодействия и ответственности
- **Standard (Стандарт)** — определяет требования к артефактам
- **Playbook (Руководство)** — определяет последовательность действий
- **Architecture (Архитектура)** — определяет структуру системы
- **Index (Индекс)** — помогает находить информацию (навигация)
- **Registry (Реестр)** — авторитетный инвентарь сущностей проекта
- **History (История)** — записывает прошлые события
- **Context (Контекст)** — описывает текущее состояние

---

## Layer Definitions (Определения слоёв)

- **Layer 0 (Meta Architecture)** — описывает саму систему знаний
- **Layer 1 (Project Identity)** — определяет идентичность проекта, роли и принципы
- **Layer 2 (Operational Knowledge)** — описывает текущее операционное состояние
- **Layer 3 (Engineering Knowledge)** — определяет, как разрабатывается и сопровождается проект
- **Layer 4 (Verification Layer)** — содержит неизменяемые артефакты, подтверждающие состояние проекта

---

## Status Definitions (Определения статусов)

- **ACTIVE (Активен)** — документ существует и поддерживается
- **PLANNED (Запланирован)** — документ запланирован, но ещё не создан
- **ARCHIVED (Архивирован)** — документ сохранён для исторической справки
- **DEPRECATED (Устарел)** — документ заменён новой версией

---

## End of Document (Конец документа)

Этот документ является каноническим реестром документов проекта.

Все добавления, удаления, архивирование или изменения статусов документов проекта должны быть отражены здесь.
