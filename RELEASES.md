# Releases: Agent Developer

## Beta-0.2.r1 (2026-06-18)

**Status:** STABLE

**Evidence:** `evidence/2026-06-17_2138_beta02r1_full.log`

**Достижения:**
- ✓ Generate: LLM генерирует Python-код
- ✓ Validate: py_compile проверяет синтаксис
- ✓ Retry: автоматическое исправление ошибок
- ✓ Success: статус completed после retry
- ✓ OpenAI-compatible API через llama-server
- ✓ Контролируемый тест retry (FORCE_INVALID_CODE_ON_FIRST_ATTEMPT)
- ✓ Типизированное состояние (ValidationResult)
- ✓ Изолированные побочные эффекты (ADR-006)
- ✓ Чистая маршрутизация (ADR-004)

**Производительность:**
- Prompt processing: 195.7 tokens/sec
- Generation: 37.5 tokens/sec

---

## Beta-0.1b (2026-06-17)

**Status:** STABLE

**Достижения:**
- ✓ Первый реальный LLM-вызов через OpenAI-compatible API
- ✓ Интеграция с llama-server (Qwen2.5-Coder-14B)
- ✓ ADR-007 подтверждён практикой

---

## Beta-0.1a (2026-06-16)

**Status:** STABLE

**Достижения:**
- ✓ Первый LangGraph вертикальный срез
- ✓ FSM retry-cycle доказан
- ✓ ADR-001, ADR-004, ADR-006 подтверждены
