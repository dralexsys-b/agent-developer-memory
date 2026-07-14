# Closure of 016.txt — Unfinished Branches (Закрытие 016.txt — Незавершённые направления работы)

**Date:** 2026-07-09
**Status:** CLOSED
**Authority:** Engineering Lead
**Canonical Source for:** Administrative closure of historical 016 issues
**Dependencies:** None
**Dependents:** None

---

## Background (Предыстория)

Файл `016.txt` документировал пять незавершённых направлений работы, которые были выявлены в ходе истории проекта. Этот документ предоставляет окончательный административный обзор каждого направления с присвоением статуса закрытия.

---

## Review of Each Unfinished Item (Обзор каждого незавершённого элемента)

### 1. Commit 5 как изолированное исправление printf

**Original goal:** Создать изолированный коммит `fix(scripts): fix printf syntax error` для исправления `printf` в `verify.sh`.

**Actual outcome:** Исправление `printf` было применено, но объединено с более крупным коммитом с исправлениями Test 9.

**Status:** **COMPLETED** (принято как единичное отклонение)

**Rationale:** Исправление применено и работает. Создание отдельного коммита на данном этапе потребовало бы переписывания истории, что не оправдано. Это отклонение принято и задокументировано.

---

### 2. Улучшения архитектуры test_publish.sh

**Original goal:** Реализовать восемь улучшений, включая `trap` cleanup, вспомогательные функции, валидацию, сброс переменных, комментарии, разделитель `tab`, git push -u origin HEAD и обработку ошибок `symbolic-ref`.

**Actual outcome:** Четыре улучшения были применены (разделитель `tab`, разделение `origin_root`, проверка `symbolic-ref`, `cleanup_temp_repo` с двумя аргументами). Четыре улучшения не были применены (`trap`, вспомогательная функция `prepare_repo`, валидация `setup_temp_repo`, сброс переменных после очистки).

**Status:** **PARTIALLY COMPLETED** — продвинутые улучшения отложены до будущего обслуживания

**Rationale:** Базовых исправлений достаточно для текущих потребностей. Оставшиеся улучшения не критичны и могут быть рассмотрены при следующей модификации скрипта.

---

### 3. Логическая атомарность Commit 6

**Original goal:** Разделить Commit 6 на отдельные коммиты для изменений `scripts/verify.sh` и изменений документации.

**Actual outcome:** Семь файлов были закоммичены вместе под `docs(runtime)`.

**Status:** **REJECTED** — история не переписана; принято как единичное отклонение

**Rationale:** Пользователь явно решил не переписывать историю. Это единичное отклонение от принципа `One Concept Per Commit` (Одна концепция на коммит). Будущие коммиты должны следовать этому принципу.

---

### 4. Documentation First для Layer 3

**Original goal:** Создать спецификацию `docs/specs/event_bus.md` перед реализацией Event Bus (следуя принципу Documentation First).

**Actual outcome:** Обсуждение было проведено, но спецификация не создана. Реализация ещё не начата.

**Status:** **MOVED** — будет выполнено в Runtime Phase 1

**Rationale:** Layer 3 (Runtime Implementation) ещё не активен. Спецификация Event Bus будет создана в рамках Runtime Phase 1, следуя принципу Documentation First.

---

### 5. Соответствие Engineering Playbook

**Original goal:** Обеспечить последовательное применение всех практик Engineering Playbook (без markdown code fences, 4-пробельный heredoc, Documentation First, TDD Red-Green-Refactor).

**Actual outcome:** Большинство практик теперь задокументированы и применяются. Markdown code fences были устранены из ответов. Форматирование heredoc стало согласованным. Оставшиеся практики соблюдаются в текущей работе.

**Status:** **COMPLETED** — практики теперь задокументированы и применяются

**Rationale:** Engineering Playbook был обновлён и используется как эталон для всех инженерных работ. Нарушения теперь рассматриваются как исключения.

---

## Summary (Резюме)

| Item (Элемент)                                                      | Status (Статус)       |
|---------------------------------------------------------------------|-----------------------|
| 1. Isolated printf fix (Изолированное исправление `printf`)         | COMPLETED             |
| 2. test_publish.sh improvements (Улучшения `test_publish.sh`)       | PARTIALLY COMPLETED   |
| 3. Atomicity of Commit 6 (Атомарность Commit 6)                     | REJECTED              |
| 4. Documentation First for Layer 3                                  | MOVED                 |
| 5. Engineering Playbook compliance (Соответствие Engineering Playbook) | COMPLETED          |

---

## Conclusion (Заключение)

Все элементы из `016.txt` были рассмотрены и получили статус закрытия. Файл теперь считается историческим и более не активным. Этот документ служит канонической записью административного закрытия.

**Next steps (Следующие шаги):**
- Перейти к Commit 11: Architecture Decision on Excluded Items (ADR для удаления Portfolio и Registry)
- Продолжить план `Program Management Completion`

---

**End of Document (Конец документа)**
