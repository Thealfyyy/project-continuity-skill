---
project: <project name>
owner: <name or team>
status: <planning | active | paused | complete — current phase>
last_updated: <YYYY-MM-DD>
---

# Project Brief: <project name>

> **Guidelines for this file:**
> - **Purpose:** `BRIEF.md` is the stable, living single source of truth for *present truth*—what the project is, why it is shaped this way, and what "done" means.
> - **What belongs here:** Locked architecture decisions, hard constraints, stack choices, explicit scope boundaries, and codebase structure.
> - **What does NOT belong here:** Routine session progress, bug-fix diaries, or inline `UPDATE:` history notes (those belong in `PROGRESS_LOG.md`). When a decision changes, rewrite the relevant section cleanly so the brief always reflects the current state.

Read this file in full before doing any work. Read `PROGRESS_LOG.md` next (most recent entries at the bottom), then `TASKS.md`, then `REQUESTS.md`.

---

## 1. What this project is
<!-- Guideline: Write 1–2 concise paragraphs covering the product goal, target users, and core problem being solved. -->
<One clear paragraph: the goal, who it is for, and why it exists.>

---

## 2. Context, deadlines, and hard constraints
<!-- Guideline: List external deadlines, regulatory/compliance rules, budget/hardware limits, or non-negotiable requirements. -->
- **Timeline / Deadlines:** <target dates or milestones>
- **Hard Constraints:** <e.g., offline-only, specific API contracts, data privacy rules, latency budgets>

---

## 3. Locked-in decisions
<!-- Guideline: Record architecture, product, or design choices that are already settled so future sessions do not re-litigate them. Include *why* each decision was made. -->
| Area | Decision | Rationale |
| :--- | :--- | :--- |
| <e.g., Database> | <e.g., PostgreSQL + pgvector> | <e.g., Single relational + vector store reduces ops overhead> |
| <e.g., Auth> | <e.g., JWT / Session> | <reason> |

---

## 4. Tech stack & tools
<!-- Guideline: List the primary languages, frameworks, databases, infrastructure, and testing tools. -->
- **Language & Runtime:** <e.g., Python 3.12>
- **Frameworks & Libraries:** <e.g., FastAPI, LangGraph, Pydantic>
- **Data & Storage:** <e.g., PostgreSQL, Redis, ChromaDB>
- **Testing & Infra:** <e.g., Pytest, Docker Compose, GitHub Actions>

---

## 5. Current scope

**In scope right now (current phase):**
<!-- Guideline: Bullet list of deliverables actively targeted for the current milestone. -->
- <Deliverable 1>
- <Deliverable 2>

**Explicitly out of scope for now (and why):**
<!-- Guideline: Naming deferred features prevents scope creep and stops an AI agent from "helpfully" building unrequested features. -->
- <Deferred feature 1> — *Deferred because: <reason>*
- <Deferred feature 2> — *Deferred because: <reason>*

---

## 6. How this project is organized
<!-- Guideline: Provide a short directory map and explain module boundaries so any new agent can navigate the repository immediately. -->
```text
project-root/
├── src/                  # Core application logic
├── tests/                # Automated test suite
└── docs/agent-context/   # Continuity files (BRIEF, TASKS, REQUESTS, PROGRESS_LOG)
```

---

## 7. Working norms & verification standards
<!-- Guideline: Define code quality expectations, testing gates, branch/commit conventions, and what must pass before marking a task done. -->
- **Definition of Done:** <e.g., all unit tests pass, linters clean, docs updated>
- **Review / Gate Rules:** <e.g., stop for human confirmation before schema migrations or external API spend>
