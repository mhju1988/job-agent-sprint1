# Implementation Plan — Automated Job Application Agent

## Goal (MVP)
Solo Python app: scrape/fetch jobs → match against my CV → generate tailored cover letter + CV variant → track in Supabase → Streamlit dashboard.

## Architecture
```
User → Streamlit UI
         │
         ▼
   CrewAI Orchestrator
   ├── Scout Agent     → Playwright/API → jobs table
   ├── Matcher Agent   → pgvector similarity → match_scores table
   ├── Writer Agent    → python-docx → applications table + .docx files
   └── Tracker Agent   → status updates, follow-up reminders
         │
         ▼
   Supabase (Postgres + pgvector) + local /artifacts/*.docx
```

## Data model (Supabase)
- `profile` (user CV: skills[], experience, education, summary, embedding)
- `jobs` (source, url, title, company, location, requirements[], description, embedding, scraped_at)
- `match_scores` (job_id, score, gaps[], rationale, created_at)
- `applications` (job_id, cover_letter_path, cv_variant_path, status, applied_at, follow_up_at)

## Sprint deliverables

### Sprint 1 — Research & Architecture
- [ ] Evaluate 3 job sources (one API, one scrape target, one fallback) — write `docs/sources.md`
- [ ] Legal note: ToS + GDPR — `docs/legal.md`
- [ ] CrewAI hello-world: 1 agent calls GWDG LLM successfully
- [ ] Supabase schema + migrations applied
- [ ] Repo skeleton + CI (ruff, mypy, pytest)

### Sprint 2 — Scout Agent
- [ ] Playwright scraper for 1 site (or API client)
- [ ] Job extraction → structured `Job` pydantic model
- [ ] Persist to Supabase; dedupe by URL
- [ ] 10 jobs fetched end-to-end in tests

### Sprint 3 — Matcher Agent
- [ ] CV PDF parser → `Profile` model
- [ ] Embeddings via GWDG; store in pgvector
- [ ] Cosine similarity + LLM gap analysis
- [ ] Top-N ranked jobs with rationale

### Sprint 4 — Writer Agent
- [ ] Cover letter template (Jinja + LLM fill)
- [ ] CV variant: re-rank/emphasize skills per job
- [ ] python-docx export → `/artifacts/`
- [ ] Quality check pass (no hallucinated experience)

### Sprint 5 — Tracker & UI
- [ ] Streamlit dashboard: jobs / matches / applications
- [ ] Status state machine: new → applied → interview → offer/rejected
- [ ] Follow-up reminder logic (n days after applied)
- [ ] Demo script + final README

## Folder layout
```
job-agent/
├── CLAUDE.md
├── PLAN.md
├── PROGRESS.md
├── pyproject.toml
├── .env.example
├── .claude/agents/         # subagent definitions
├── src/job_agent/
│   ├── agents/             # scout, matcher, writer, tracker
│   ├── tools/              # playwright, docx, supabase, gwdg_llm
│   ├── models/             # pydantic schemas
│   ├── db/                 # supabase client + migrations
│   └── ui/                 # streamlit
├── tests/
├── artifacts/              # generated .docx (gitignored)
└── docs/
```

## Done = sprint tagged in git + PROGRESS.md updated + demo recorded.
