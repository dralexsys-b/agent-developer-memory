# Repositories Registry (Реестр репозиториев)

**Status:** ACTIVE
**Version:** 1.0
**Date:** 2026-06-18
**Authority:** Infrastructure Lead
**Maintainer:** Infrastructure Maintainer

**Type:** Registry (Layer 2: Operational Knowledge)
**Primary Question:** "Where is the code?"
**Canonical Source for:** Complete registry of project repositories
**Dependencies:** INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md
**Dependents:** CODE_INDEX.md, CURRENT_CONTEXT.md, DOCUMENTS.md

---

## Relationships (Связи)

**Dependencies (Зависимости):**
- INFORMATION_ARCHITECTURE.md
- PROJECT_PROTOCOL.md

**Dependents (Зависимые документы):**
- CODE_INDEX.md
- CURRENT_CONTEXT.md
- DOCUMENTS.md

---

## Registry (Реестр)

| Repository (Репозиторий)  | Purpose (Назначение)                         | URL                                                    | Default Branch (Ветка по умолчанию) | Baseline            | Owner (Владелец)    | Status (Статус) |
|---------------------------|----------------------------------------------|--------------------------------------------------------|-------------------------------------|---------------------|---------------------|-----------------|
| `agent-developer-runtime` | Исходный код, оркестраторы, инструменты      | https://github.com/dralexsys-b/agent-developer-runtime | main                                | agent-dev-v0.2.0-r1 | Infrastructure Lead | ACTIVE          |
| `agent-developer-memory`  | Документация, ADR, доказательства, протоколы | https://github.com/dralexsys-b/agent-developer-memory  | main                                | agent-dev-v0.2.0-r1 | Documentation Lead  | ACTIVE          |

---

## Repository Layout (Структура репозиториев)

### agent-developer-memory

**Ключевые каталоги:**
- `evidence/` — неизменяемые артефакты верификации (логи, результаты тестов, бенчмарки)
- `adr/` — записи архитектурных решений (планируется)

**Примечание:** Структура репозитория определена здесь. Детальный инвентарь файлов поддерживается в `CODE_INDEX.md`.

### agent-developer-runtime

**Ключевые каталоги:**
- `src/` — исходный код (оркестраторы, инструменты)
- `tests/` — тестовые файлы (планируется)

**Примечание:** Структура репозитория определена здесь. Детальный инвентарь файлов поддерживается в `CODE_INDEX.md`.

---

## Repository Rules (Правила репозиториев)

1. **agent-developer-runtime** содержит только исполняемый код и runtime-артефакты
2. **agent-developer-memory** содержит только документацию, протоколы и доказательства
3. Файлы доказательств неизменяемы и никогда не модифицируются после создания
4. Документация следует структуре, определённой в INFORMATION_ARCHITECTURE.md
5. Все изменения в репозиториях требуют доказательств (логи, результаты тестов)

---

## Status Definitions (Определения статусов)

- **ACTIVE (Активен)** — репозиторий активно поддерживается
- **ARCHIVED (Архивирован)** — репозиторий сохранён, но больше не активно разрабатывается
- **DEPRECATED (Устарел)** — репозиторий заменён новым репозиторием

---

## End of Document (Конец документа)

Этот документ является каноническим реестром репозиториев проекта.

Все добавления, удаления или изменения статусов репозиториев проекта должны быть отражены здесь.
