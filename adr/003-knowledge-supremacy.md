# ADR-003: Knowledge Supremacy Matrix (Иерархия доверия)

**Статус:** AGREED_DESIGN (Design agreed, implementation not verified)  
**Дата:** 2024-06-16

## Контекст
Существует риск рассинхронизации между векторной базой данных (Qdrant) и реальной файловой системой.

## Решение
Согласован приоритет при разрешении конфликтов:
1. Artifact Graph / File System (Ground Truth)
2. ADR Registry
3. Skill Registry
4. Memory Layer (Qdrant) (Только семантический индекс).

## Последствия
Дизайн утверждён. Реализация и проверка этого правила в коде оркестратора ещё не выполнены.
