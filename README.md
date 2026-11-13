# Project Continuity Skill (`project-continuity`)

A lightweight, **agent-agnostic** skill for maintaining persistent project context across coding sessions and across different AI coding agents (**Antigravity, Claude Code, Codex, Cursor, Windsurf**, or any agentic workflow).

Instead of relying on ephemeral chat histories or proprietary memory tools, `project-continuity` uses **four plain, version-controlled Markdown files** stored in `docs/agent-context/` at the root of your repository.

---

## Why Use This?

1. **Zero Context Loss Across Chats & Tools:** Start a feature in Claude Code, debug it in Antigravity, and review it in Codex—every agent reads the same ground truth at startup and leaves an exact handoff note before ending.
2. **Separates "Present Truth" from "Session History":** Architecture decisions stay clean in `BRIEF.md`, active checklists live in `TASKS.md`, and session-by-session history is appended to `PROGRESS_LOG.md`.
3. **Captures Human Ideas Safely:** `REQUESTS.md` gives you a structured place to jot down new feature ideas without losing them inside random chat prompts or triggering unplanned scope creep.

---

## The Four Continuity Files (`docs/agent-context/`)

| File | Purpose | Update Rule |
| :--- | :--- | :--- |
| **`BRIEF.md`** | What the project is, deadlines, locked architecture decisions, scope boundaries, and codebase map. | Rewrite in place only when a real decision or scope boundary changes. |
| **`TASKS.md`** | Phase-gated checklist (`[ ]` todo, `[~]` in progress, `[x]` done, `[!]` blocked). | Updated in real time as tasks complete. |
| **`REQUESTS.md`** | Human-written feature/change intake (`New` → `Queued` → `Done`). | Agent never rewrites your `Description` or `Why`—only adds `Status` and `Triage note`. |
| **`PROGRESS_LOG.md`** | Session-by-session engineering diary (what was done, why, what broke, how it was fixed, what's next). | **Append-only.** Newest entry at the bottom. |

---

## Quick Installation

### Option 1: Copy into Your Agent's Skills Directory
Clone or copy this folder into your workspace or global agent skills directory:
- **Antigravity / Codex / Universal:** `.agents/skills/project-continuity/`
- **Claude Code:** `.claude/skills/project-continuity/`
- **Cursor:** `.cursor/skills/project-continuity/`

### Option 2: Install via `.skill` Package
Use the pre-packaged [`project-continuity.skill`](project-continuity.skill) archive included in this repository.

---

## Usage

Once installed, simply prompt your AI coding agent on any new or existing project:
> *"Set up project continuity tracking for this repo."*

At the start of every new session, point the agent to `docs/agent-context/` (or simply ask it to read the continuity files), and before wrapping up a session, ask it to update `TASKS.md` and append a session entry to `PROGRESS_LOG.md`.

---

## License

MIT License — feel free to use, modify, and share. See [LICENSE](LICENSE).
