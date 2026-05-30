---
name: groundwork-resume
description: Session pause and resume protocol for any learning project. Use this when the user says "pause", "I'm stopping", "let's continue later", "resume", "continue [project]", "where did we leave off", or starts a session that picks up prior learning. Handles both sides of the boundary — writing a clean checkpoint before stopping, and reading the trail to resume cold.
---

# Groundwork: Resume

Learning spans multiple sessions. A new conversation has no memory of the previous one — continuity comes entirely from the trail on disk (`git log`, `notes.md`, the README checklist). The job at session boundaries is to keep that trail complete enough to resume cold.

## On pause — "I'm stopping" / "let's continue later"

Before the session ends:

1. **Write a `notes.md` entry** for what was covered in this session. End with a concrete `Next:` line — one sentence naming the exact next concept or step. This is the handoff for the next session.
2. **Commit everything** — working code, notes.md, any updated files. The git log marks the stopping point.
3. **If anything is concept-worthy:** create or update the relevant concept note and link it from the project README. Don't leave theory in conversation — only files persist.

Never end a session with unwritten learning. If a step's work isn't in `notes.md` and committed, it is lost.

### notes.md entry format

```
## YYYY-MM-DD

**What we covered:** [one-line summary]
**What worked:** [anything notable]
**What broke / open questions:** [issues or things to investigate]
**Next:** [exact next concept or step — specific enough to pick up cold]
```

## On resume — "resume" / "continue [project]" / "where did we leave off?"

Before writing any new code:

1. **Read the trail:**
   - `notes.md` — newest entry and its `Next:` line
   - README **Approach** checklist — `[x]` done vs `[ ]` pending
   - `git log --oneline` — last few commits
2. **Summarise in 2–3 lines** — last step done, what broke, what's next.
3. **Confirm with the learner** before writing any code. Don't assume the `Next:` line is still the right direction — they may have changed their mind.
4. **Continue from the `Next:` line.** Do not re-run or re-explain completed steps.

### If no project is named

Check which project has the most recent commit and offer to resume that one.

```bash
# find most recently committed project
find . -name ".git" -maxdepth 3 | xargs -I{} dirname {} | xargs -I{} git -C {} log -1 --format="%ci %H" 2>/dev/null | sort -r | head -5
```
