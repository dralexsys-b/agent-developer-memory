# Code Index: Agent Developer

> **Правило:** Файл получает статус `EXISTS` только после прямого подтверждения в `evidence/`.
> **Примечание:** Пути указаны относительно корня проекта `~/agent-dev/`. Runtime-код находится в отдельном репозитории `agent-developer-runtime/`.

## 🟢 Existing Files (EXISTS)

| File Path | Purpose | Status | Evidence Link |
| :-- | :-- | :-- | :-- |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_1a.py` | Beta-0.1a vertical slice (LangGraph 1.2.0) | EXISTS | `evidence/2026-06-16_1425_beta01a_run.log`, `evidence/2026-06-16_1800_beta01a_repro_run.log` |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_1b.py` | Beta-0.1b LLM integration (OpenAI-compatible API) | EXISTS | `evidence/2026-06-17_1808_beta01b_full.log` |
| `agent-developer-runtime/src/orchestrator_v2_beta_0_2.py` | Beta-0.2.r1 Generate → Validate → Retry → Success | EXISTS | `evidence/2026-06-17_2138_beta02r1_full.log` |
| `INFORMATION_ARCHITECTURE.md` | Meta Architecture — фундамент системы знаний проекта | EXISTS | N/A (Root document) |
| `PROJECT_PROTOCOL.md` | Project Protocol — роли, принципы, источники истины | EXISTS | Based on: INFORMATION_ARCHITECTURE.md |
| `PROJECT_GOVERNANCE.md` | Project Governance — constitution, vision, products, goals, phases, invariants, principles, governance process, change classification | EXISTS | Based on: DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md, TASK_LIFECYCLE.md |
| `DOCUMENTS.md` | Documents Registry — единый каталог документов | EXISTS | Based on: INFORMATION_ARCHITECTURE.md |
| `REPOSITORIES.md` | Repositories Registry — каталог репозиториев | EXISTS | Based on: INFORMATION_ARCHITECTURE.md |
| `ENGINEERING_PLAYBOOK.md` | Engineering Playbook — procedures, workflow, best practices | EXISTS | Based on: PROJECT_PROTOCOL.md |
| `DOC_STANDARD.md` | Documentation Standard — formatting, structure, quality requirements | EXISTS | Based on: ENGINEERING_PLAYBOOK.md |
| `RELEASE_PROCESS.md` | Release Process — release procedures, versioning, deployment | EXISTS | Based on: ENGINEERING_PLAYBOOK.md, DOC_STANDARD.md |
| `AUTOMATION.md` | Automation — scripts, registry, structure, triggers | EXISTS | Based on: ENGINEERING_PLAYBOOK.md, RELEASE_PROCESS.md |
| `ENGINEERING_HISTORY.md` | Engineering History — lessons learned, post-mortems, retrospectives | EXISTS | Based on: ENGINEERING_PLAYBOOK.md |
| `DOMAIN_ARCHITECTURE.md` | Domain Architecture — entities, contracts, relationships, state models, event model | EXISTS | Based on: INFORMATION_ARCHITECTURE.md, PROJECT_PROTOCOL.md |
| `SYSTEM_BOUNDARIES.md` | System Boundaries — services, runtime, storage, projections, agent implementations | EXISTS | Based on: DOMAIN_ARCHITECTURE.md |
| `TASK_LIFECYCLE.md` | Task Lifecycle — stages, transitions, quality gates, failure paths | EXISTS | Based on: DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md |
| `LAYER3_ROADMAP.md` | Layer 3 Roadmap — план реализации Runtime, итерации, Vertical Slice | EXISTS | Based on: DOMAIN_ARCHITECTURE.md, SYSTEM_BOUNDARIES.md, TASK_LIFECYCLE.md, PROJECT_GOVERNANCE.md |

## 🟠 Candidates (CANDIDATES)

| File Path | Purpose | Status |
| :-- | :-- | :-- |
| `tools.py` | Минимальный автономный Tool Layer | CANDIDATE (отложено до Beta-1 согласно ADR-006) |
| `start_Agent_Dev.sh` | Скрипт запуска LLM-серверов | CANDIDATE |
| `stop_Agent_Dev.sh` | Скрипт остановки LLM-серверов | CANDIDATE |
| `orchestrator_v2_beta_0_2.py` | LangGraph оркестратор Beta-0.2 (с реальным LLM) | CANDIDATE |
| `test_filestate_fsm.py` | Изолированные тесты FSM v1.3 | CANDIDATE (требуется для перевода ADR-002 в ACCEPTED) |
