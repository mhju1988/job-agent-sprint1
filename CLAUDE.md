# Automated Job Application Agent — Project Rules

## Context
University course "Agentic AI" (W-HS). Solo project, 5 sprints, 20h/week.
Spec source: `../AAI_ Projektvorschläge _ Moodle.pdf` → Project #7.

## Stack (fixed — do not substitute)
- Python 3.11+, `uv` for env mgmt
- **CrewAI** multi-agent (Scout, Matcher, Writer, Tracker)
- **Playwright** for scraping (fallback: Adzuna/JSearch API)
- **python-docx**, **pypdf** for documents
- **Supabase** (Postgres + pgvector) for persistence
- **GWDG LLM endpoint** (OpenAI-compatible) — never call paid APIs
- **Streamlit** for UI (sprint 5)

## Code rules
- Type hints everywhere; `pydantic` for all LLM I/O schemas
- One module per agent under `agents/`; tools under `tools/`
- No secrets in code — use `.env` + `pydantic-settings`
- Tests with `pytest`; mock LLM + scraper calls
- Pre-commit: `ruff`, `mypy`

## Token efficiency rules for Claude Code
1. **Always read `PLAN.md` first** before any task — it is the source of truth
2. Delegate large file reads / web research to **subagents** (see `.claude/agents/`)
3. Use the `superpowers:brainstorming` skill before any new feature
4. Use the `superpowers:test-driven-development` skill for all code
5. Use the `superpowers:writing-plans` skill before multi-step work
6. Never paste raw scraper HTML or full PDFs into context — summarize via subagent
7. After every sprint: update `PROGRESS.md` (one paragraph)

## Sprint gates
Sprint complete only when: deliverable demoed + tests green + **`code-reviewer` subagent run with no 🔴 blockers** + `PROGRESS.md` updated + commit tagged `sprint-N`.

## Out of scope
- Auto-submitting applications (manual click only — ToS/GDPR)
- LinkedIn/Indeed scraping if ToS forbids → use API
- Multi-user, hosting, mobile
