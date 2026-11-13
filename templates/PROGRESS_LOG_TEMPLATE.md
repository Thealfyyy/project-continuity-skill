---
project: <project name>
purpose: append-only log of what actually happened, session by session
---

# Progress Log

**How to use this file:** append-only, newest entry at the bottom, one
entry per work session. Never edit or delete a past entry — if an
earlier approach turned out wrong, say so in a new entry. Read from the
bottom upward at the start of a session until you have enough context.

---

## Entry template (copy this for each new entry)

```
## Session N — <date> — <agent/tool used>

**Worked on:** <which tasks from TASKS.md>

**What was done:**
- <bullet per concrete thing completed>

**How it was done:**
- <key implementation choices and why>

**What broke / went wrong:**
- <bugs, blockers, wrong assumptions — or "nothing notable">

**How it was fixed (or: still unresolved):**
- <resolution, or flag as unresolved + what's needed to unblock it>

**What's next:**
- <specific handoff note for the next session>
```

---

## Session 0 — <date> — Planning

**Worked on:** Initial scoping.

**What was done:**
- <what was decided in the planning session>

**How it was done:**
- <reasoning behind the initial scope/approach>

**What broke / went wrong:**
- N/A — no work executed yet.

**How it was fixed:**
- N/A.

**What's next:**
- <first concrete task to start with>
