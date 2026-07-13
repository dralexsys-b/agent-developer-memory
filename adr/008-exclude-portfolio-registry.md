# ADR 008: Exclude Program Portfolio and Program Registry from Program Recovery (ADR 008: Исключить Program Portfolio (Портфолио программ) и Program Registry (Реестр программ) из Program Recovery (Восстановление программы))

**Date:** 2026-07-09
**Status:** ACCEPTED
**Authority:** Engineering Lead

**Context:** Program Recovery v1 (Восстановление программы v1) первоначально включал Commit 10 (Program Portfolio) и Commit 11 (Program Registry). В ходе выполнения стало ясно, что они не требуются для текущей фазы.

## Decision (Решение)

Исключить Commit 10 (Program Portfolio) и Commit 11 (Program Registry) из Program Recovery v1.

## Rationale (Обоснование)

- Program Portfolio (Портфолио программ) — это концепция управления более высокого уровня, не нужная для текущего масштаба проекта (всего несколько программ).
- Program Registry (Реестр программ) — это деталь реализации PROGRAMS.md, а не отдельная концепция управления.
- Сохранение этих коммитов добавило бы ненужную сложность без немедленной выгоды.
- Текущая фаза проекта фокусируется на установлении базового управления программами, а не на продвинутом управлении портфолио.

## Impact (Влияние)

- Program Recovery v1 сокращён с 20 до 18 коммитов (удаление Commit 10–11).
- PROGRAMS.md будет создан в Phase 2 без отдельного документа Registry.
- Решение документировано для предотвращения путаницы в будущем.

## Alternatives Considered (Рассмотренные альтернативы)

1. Сохранить оба коммита — отклонено из-за избыточного проектирования.
2. Объединить Program Portfolio и Program Registry в PROGRAMS.md — принято как выбранный подход.

## Related Documents (Связанные документы)

- PROGRAM_MANAGEMENT.md — определяет фреймворк управления программами.
- PROGRAMS.md — будет содержать реестр программ напрямую.
