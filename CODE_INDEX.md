# Code Index: Agent Developer

> **Правило:** Файл получает статус `EXISTS` только после прямого подтверждения в `evidence/`.
> **Примечание:** Пути указаны относительно корня проекта `~/agent-dev/`. Runtime-код находится в отдельном репозитории `agent-developer-runtime/`.

## 🟢 Existing Files (EXISTS)
| File Path | Purpose | Status | Evidence Link |
| :--- | :--- | :--- | :--- |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_1a.py` | Beta-0.1a vertical slice (LangGraph 1.2.0) | EXISTS | `evidence/2026-06-16_1425_beta01a_run.log`, `evidence/2026-06-16_1800_beta01a_repro_run.log` |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_1b.py` | Beta-0.1b LLM integration (OpenAI-compatible API) | EXISTS | `evidence/2026-06-17_1808_beta01b_full.log` |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_2.py` | Beta-0.2.r1 Generate → Validate → Retry → Success | EXISTS | `evidence/2026-06-17_2138_beta02r1_full.log` |
| `INFORMATION_ARCHITECTURE.md` | Meta Architecture — фундамент системы знаний проекта | EXISTS | Architecture |

## 🟡 Planned Files (PLANNED)
| File Path | Purpose | Status |
| :--- | :--- | :--- |
| *(пусто)* | *(Решения о создании ещё не приняты)* | - |

## 🟠 Candidates (CANDIDATES)
| File Path | Purpose | Status |
| :--- | :--- | :--- |
| `tools.py` | Минимальный автономный Tool Layer | CANDIDATE (отложено до Beta-1 согласно ADR-006) |
| `start_Agent_Dev.sh` | Скрипт запуска LLM-серверов | CANDIDATE |
| `stop_Agent_Dev.sh` | Скрипт остановки LLM-серверов | CANDIDATE |
| `orchestrator_v2_beta_0_2.py` | LangGraph оркестратор Beta-0.2 (с реальным LLM) | CANDIDATE |
| `test_filestate_fsm.py` | Изолированные тесты FSM v1.3 | CANDIDATE (требуется для перевода ADR-002 в ACCEPTED) |
