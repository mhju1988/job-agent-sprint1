# Automated Job Application Agent

Solo university project (W-HS "Agentic AI"). Scrapes/fetches jobs, matches against a CV, generates tailored cover letter + CV variant, tracks progress in Supabase, and surfaces it in a Streamlit dashboard.

See `PLAN.md` for sprint-by-sprint deliverables and `CLAUDE.md` for development rules.

## Setup

```powershell
uv sync
copy .env.example .env   # then fill in GWDG + Supabase keys
uv run pre-commit install
uv run pytest
```

## Stack
Python 3.11 · CrewAI · Playwright · python-docx · pypdf · Supabase (Postgres + pgvector) · GWDG LLM · Streamlit
