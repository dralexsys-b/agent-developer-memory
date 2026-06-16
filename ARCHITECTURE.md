# Architecture: Agent Developer

> **Правило:** Этот файл описывает текущие проектные договорённости. Причины решений ("почему") формализованы в каталоге `adr/`.

## 1. Knowledge Supremacy Matrix
При разрешении конфликтов агент строго следует приоритету:
1. **Artifact Graph / File System** (Ground Truth)
2. **ADR Registry**
3. **Skill Registry**
4. **Memory Layer (Qdrant)** (Только семантический индекс)
*(См. [ADR-003](adr/003-knowledge-supremacy.md))*

## 2. FileState FSM v1.3
- **Состояния:** `pending` → `generating` → `writing` → `validating` → `completed` | `failed`
- **Семантика Retries:** `retries` считает только *повторные* попытки. Общее число = `max_retries + 1`.
- **Инвариант:** `retries` увеличивается **только** при ошибке валидации и если `< max_retries`.
*(См. [ADR-002](adr/002-filestate-fsm-v1.3.md))*

## 3. LangGraph Routing Rules
- **Чистота Router:** Узлы маршрутизации возвращают только строку (имя следующего узла). Вся мутация состояния происходит строго в узлах обработки.
*(См. [ADR-004](adr/004-pure-router.md))*

## 4. Правила каталога evidence/
- Хранение сырых, неинтерпретированных результатов.
- Именование: `YYYY-MM-DD_HHMM_<type>.log`.
*(См. [ADR-005](adr/005-lean-memory-architecture.md))*
