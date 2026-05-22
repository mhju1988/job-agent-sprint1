# Start Prompt for Claude Code

Paste this as the **first message** in a fresh Claude Code session inside `job-agent/`.

---

You are helping me build the Automated Job Application Agent — a solo university project (5 sprints).

Before doing anything:
1. Read `CLAUDE.md` and `PLAN.md` in full
2. Confirm you understand the stack, sprint structure, and token-efficiency rules
3. Check `PROGRESS.md` (create it if missing) to see current sprint state

Then propose the next concrete step (single sprint task, not the whole sprint).

Rules of engagement:
- Use the `superpowers:brainstorming` skill before any design decision
- Use `superpowers:writing-plans` before any multi-file change
- Use `superpowers:test-driven-development` for all code
- Delegate to subagents:
  - `scraper-researcher` for any job-site investigation
  - `doc-summarizer` for any file > 200 lines or any PDF
  - `crewai-implementer` for agent-module work
  - `code-reviewer` after every implementation task and before each sprint tag
- Never read full PDFs or scraped HTML in the main thread
- Never call paid LLM APIs — only the GWDG endpoint via env vars
- Ask me before introducing a new dependency

Start by reading the two files and giving me a 5-line status + proposed next step.
