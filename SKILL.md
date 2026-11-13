---
name: project-continuity
description: Maintain persistent project context across work sessions and across different coding agents (Antigravity, Claude Code, Codex, or any other agentic tool) using four tracked plain-Markdown files — a project brief, a task list, a feature/change request intake, and an append-only progress log — stored in a project's docs/agent-context/ folder. Use this skill at the START of any coding session on a tracked project (read all four files before doing anything else) and at the END of any session with real progress (update the task list, triage any new requests, and append a log entry). Also use this skill when a NEW project should adopt this tracking system, when the user asks to "set up project tracking," "keep context between sessions," "hand off to another agent," "log a feature request," or wants a way to avoid re-explaining project context every time they start a new chat or switch tools. Push to use this proactively whenever multi-session or multi-tool continuity is at stake — don't wait to be asked explicitly.
---

# Project Continuity

The problem this solves: an agent session (or an agent *tool* — you might
be Antigravity today and Claude Code next week on the same project) has no
memory of what happened last time unless it's written down somewhere both
agents can read. Chat history doesn't transfer between tools. It also
solves a second, related problem: the human's own new ideas and feature
requests tend to get typed straight into an agent's chat box as
unstructured prompts and then lost — this skill gives them a durable,
structured place to write those down instead, separate from the agent's
own task tracking. This skill is the transfer mechanism for both: four
plain Markdown files, agent-agnostic, version-controlled alongside the
code, that any agent reads at the start of a session and writes to at
the end.

This is deliberately low-tech: no special tooling, no agent-specific
syntax, no database. Just four files any agent (or human) can open and
read directly.

## The four files

All four live in `docs/agent-context/` at the root of the project repo.

### 1. `BRIEF.md` — what the project is, and why

The stable, "living but rarely rewritten" file. Contains: what the
product/project is, business context and deadlines, locked-in
architecture or design decisions, tech stack, **current scope**
(explicitly what's in scope right now vs. deliberately deferred and
why), and pointers to how the work is organized (directory structure,
module boundaries, whatever's relevant to the project type).

- Update this when a real decision changes (scope shifts, a deadline
  moves, an architecture choice is reversed) — not for routine progress.
- When scope changes, say so explicitly and note *why* — the reasoning
  belongs in the log too, but the current state belongs here.
- Keep it current, not historical. If something is no longer true,
  rewrite that section rather than appending "UPDATE:" notes inline —
  the log is where history lives, the brief is where present truth
  lives.

### 2. `TASKS.md` — what needs doing, and current status

A checklist, organized however makes sense for the project (by day, by
milestone, by feature — match the project's actual rhythm). Each task
uses one of four states:

- `[ ]` not started
- `[~]` in progress
- `[x]` done
- `[!]` blocked — explain the blocker inline, and log it in
  `PROGRESS_LOG.md` with detail

Update checkboxes in the same session the work happens — don't let this
drift out of sync with reality. If you finish a task, check it off
immediately, not "at the end of the session" (sessions get interrupted).

### 3. `REQUESTS.md` — new features/changes the human wants, before they're tasks

Written primarily **by the human**, not the agent. This is the intake
point for new ideas — instead of typing a feature request straight into
the agent's chat box as an unstructured prompt (where it's easy to
under-specify and easy to lose), the human writes it here with room to
actually elaborate: what they want, why, and any acceptance criteria,
using the entry template below.

- **Not append-only** (unlike the progress log) — it's a working list,
  like `TASKS.md`. Entries move through statuses: `New` → `Queued` →
  `Done` (or stay `New` with a triage question if unclear).
- The agent's job each session: read any `New` entries, and either (a)
  turn each into one or more tasks in `TASKS.md`, set the request's
  status to `Queued`, and note which task(s) it became, or (b) if the
  request is ambiguous or conflicts with current scope in `BRIEF.md`,
  leave it `New` and add a specific question or conflict note rather
  than guessing at what was meant.
- **The agent must never rewrite the human's `Description` or `Why`
  fields.** Only the `Status` field and a `Triage note` the agent adds
  are agent-editable — the human's own words stay untouched, the same
  way past log entries stay untouched.
- Once the linked task is actually completed, mark the request `Done`.

Entry template:

```
## REQ-<n> — <short title> — <date written>

**Status:** New

**Type:** Feature | Change | Bug fix | Question / investigation

**Description:**
<what the human wants, in their own words>

**Why:**
<what problem this solves, or why it matters now>

**Acceptance criteria (optional):**
- <how they'll know this is actually done>

**Notes (optional):**
<constraints, things to avoid, related existing code/areas>

**Triage note (agent-editable, doesn't touch the fields above):**
<e.g. "Queued as Day 4 task" or "Unclear — confirm X vs Y" or
"Conflicts with BRIEF.md §5, confirm before building">
```

### 4. `PROGRESS_LOG.md` — what actually happened, session by session

**Append-only.** Never edit or delete a past entry. If a past approach
turned out to be wrong, say so in a *new* entry — the log is a history,
not a status board (that's what `TASKS.md` is for). Newest entry at the
bottom, chronological top to bottom.

Each entry follows this template:

```
## Session N — <date> — <agent/tool used>

**Worked on:** <which tasks from TASKS.md>

**What was done:**
- <bullet per concrete thing completed>

**How it was done:**
- <key implementation choices and why — enough for someone with zero
  prior context to understand the reasoning, not just diff the code>

**What broke / went wrong:**
- <bugs, blockers, wrong assumptions — or "nothing notable" explicitly,
  don't just omit the section>

**How it was fixed (or: still unresolved):**
- <resolution, or flag as unresolved + what's needed to unblock it>

**What's next:**
- <specific handoff note for the next session — "continue Day 3" is too
  vague; name the actual next concrete step>
```

Write an entry for every session with real progress, however short.
Skipping entries is what breaks continuity — the whole point is that no
session should end without leaving a trail.

## Workflow

**At the start of any session on a tracked project:**

1. Read `BRIEF.md` in full.
2. Read `PROGRESS_LOG.md` starting from the bottom (most recent) and
   read upward until you have enough context — usually the last 1–3
   entries, more if the project has been idle a while or you're a new
   agent tool being introduced to the project for the first time.
3. Read `TASKS.md` to see current status.
4. Read `REQUESTS.md` and triage any `New` entries (see §3 above)
   before starting other work — the human may have queued up new
   scope since the last session.
5. Do not re-derive or re-decide anything already settled in `BRIEF.md`
   or already logged as tried-and-failed in `PROGRESS_LOG.md` — if an
   approach was already attempted and reversed, don't propose it again
   without acknowledging that history.

**During the session:** update `TASKS.md` checkboxes as work completes,
in real time, not retroactively. If a `REQUESTS.md` item gets fully
built during the session, mark it `Done` there too.

**Before ending any session with real progress:** append one entry to
`PROGRESS_LOG.md` using the template above. If a scope or architecture
decision changed, update `BRIEF.md` too and say so in the log entry.

## Setting up a new project with this system

When asked to set up this tracking system for a new project:

1. Create `docs/agent-context/` in the project.
2. Copy `templates/BRIEF_TEMPLATE.md`, `templates/TASKS_TEMPLATE.md`,
   `templates/REQUESTS_TEMPLATE.md`, and
   `templates/PROGRESS_LOG_TEMPLATE.md` from this skill into that
   folder, renamed to `BRIEF.md`, `TASKS.md`, `REQUESTS.md`, and
   `PROGRESS_LOG.md`.
3. Fill in `BRIEF.md` from whatever context the user gives you — ask
   for what's missing rather than inventing decisions (deadlines,
   architecture choices, and scope boundaries should come from the
   user, not be assumed).
4. Break the near-term work into `TASKS.md`.
5. Leave `REQUESTS.md` empty aside from its template/instructions — it
   fills up as the human adds ideas, it isn't seeded by the agent.
6. Seed `PROGRESS_LOG.md` with a "Session 0" entry documenting the
   planning session itself (what was decided and why), even though no
   code was written yet — this gives the first real coding session
   something to read.
7. Tell the user these four files are now the continuity mechanism:
   any agent, in any tool, starting fresh on this project should be
   pointed at `docs/agent-context/` first, and new feature ideas go in
   `REQUESTS.md` instead of a chat prompt.

## Why this stays agent-agnostic

Nothing in these files assumes a specific tool's memory system, function
names, or conventions. That's intentional — the same four files should
work whether the next session is you, a different agent, or a different
underlying model entirely. Don't add tool-specific instructions (e.g.
"call function X") into `BRIEF.md`, `REQUESTS.md`, or the log; keep
everything as plain project/engineering context that any capable coding
agent could act on.
