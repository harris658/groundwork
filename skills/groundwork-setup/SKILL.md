---
name: groundwork-setup
description: Scaffold a complete Groundwork learning workspace from scratch. Use this when the user says "groundwork setup", "set up a learning workspace", "create a lab workspace", "initialize a groundwork workspace", or wants to start a structured learning environment. Creates the full directory structure — projects, concept library, project template, portfolio hub, and a CLAUDE.md that wires in the groundwork skills.
---

# Groundwork: Setup

Scaffolds a complete learning workspace — the same structure used in the Groundwork system. After setup, the workspace is ready to start learning concept-by-concept with the other Groundwork skills.

## Protocol

1. **Ask two questions** (if not already answered):
   - Where should the workspace be created? (path)
   - What do you want to call it? (used in the README title and CLAUDE.md)

2. **Create the directory structure** (see below).

3. **Confirm** what was created and what to do next:
   > "Workspace created at `<path>`. Open it in Claude Code and start with `groundwork-teach` when you're ready to learn something."

## Directory structure to create

```
<workspace>/
├── CLAUDE.md               # workspace config — wires groundwork skills, reference sources
├── README.md               # portfolio hub — tracks table + learning tracks
├── .gitignore              # ignores .env, data/, projects/
├── .env.example            # API key template (user fills in)
├── concepts/               # durable theory library
│   ├── README.md           # concept index
│   └── _template.md        # skeleton for a new concept note
├── _template/              # copy this to projects/<name> for each new project
│   ├── README.md
│   ├── notes.md
│   ├── requirements.txt
│   ├── src/
│   │   └── .gitkeep
│   └── data/
│       └── .gitkeep
├── docs/                   # specs, design docs
│   └── .gitkeep
├── data/                   # shared corpora reused across projects
│   └── .gitkeep
└── projects/               # individual project repos (each is its own git repo)
    └── .gitkeep
```

## File contents to write

### `CLAUDE.md`

```markdown
# <workspace-name>

A concept-by-concept learning workspace using the Groundwork system.

## Skills

- **Teaching sessions:** invoke `groundwork-teach` — handles theory-before-practice, per-step flow, debrief.
- **Pause / resume:** invoke `groundwork-resume` — checkpoints the session and reads the trail to resume cold.
- **Diagrams:** invoke `groundwork-wireframe` — draws an Excalidraw diagram after a concept is confirmed working.
- **New project:** copy `_template/` to `projects/<name>`, `git init`, fill in README, wire into hub.

## Reference sources

<!-- Fill in your reference sources here. Examples:
- A Zeno wiki with an MCP: use mcp__zeno-wiki__search_wiki / mcp__zeno-wiki__get_page
- A NotebookLM notebook: use the notebooklm skill, specify the notebook ID
- YouTube + transcript: drop into projects/<name>/references/ and cite in README
- A paper or tutorial: link in the project README
Before teaching any concept, confirm what the source is and pull from it first.
-->

## Layout

- `concepts/` — durable theory notes, one per concept. The connective tissue across projects.
- `projects/` — individual learning projects (each is its own git repo, not tracked here).
- `_template/` — skeleton for a new project. Copy it, don't modify it.
- `data/` — shared corpora reused across projects (gitignored if large).
- `docs/` — specs and design docs.

## Working inside a project

- Move concept by concept. Don't skip ahead.
- Commit after every working step. Push after every commit. Git history is the learning log.
- After each step's theory half, capture the concept in `concepts/` if it's new.
- Use `groundwork-resume` to pause or resume any project.

## Status legend

🟢 done · 🟡 in progress · ⚪ planned
```

### `README.md`

```markdown
# <workspace-name>

A hands-on learning workspace. Each project is built concept-by-concept from a reference source. The goal is practical understanding, not polish.

## Portfolio

| Project | Track | Status | Headline |
|---------|-------|--------|---------|
| | | ⚪ | |

## Learning Tracks

### Standalone
Projects that don't fit a named track yet.

---

*Hub last updated: <date>*
```

### `.gitignore`

```
.env
data/
projects/
```

### `.env.example`

```
# API keys for this workspace
# Copy to .env and fill in — never commit .env

# OPENAI_API_KEY=
# ANTHROPIC_API_KEY=
```

### `concepts/README.md`

```markdown
# Concept Library

Durable theory — the ideas behind the projects, in plain English. One note per concept. Each links to where it was practiced and to adjacent concepts.

Unlike a project's `notes.md` (a session log), a concept note is the thing you want to still understand in six months.

## Concepts

| Concept | One-liner | Practiced in |
|---------|-----------|--------------|
| | | |

## To capture

Concepts touched in sessions but not yet written up:
- 
```

### `concepts/_template.md`

```markdown
# <Concept>

> One line, plain English: what it is.

**Status:** `learned | exploring`

## What it is

2–4 sentences. Assume you're explaining it to yourself in six months. No jargon without a definition.

## Why it exists / the problem it solves

The gap it fills — ideally framed against the concept that came before it. What was broken that made someone invent this?

## Mental model

An analogy or one-liner that makes it click.

## Where I practiced it

- [<project-name>](../projects/<project-name>/) — what I built, the headline result.

## Gotchas I hit

Real failure modes from the sessions.

-

## Related concepts

-
```

### `_template/README.md`

```markdown
# <project-name>

> One-line description of the concept this project explores.

## Showcase

> Fill this when the project hits a showcase-worthy milestone.

- **What this proves:** `<capability>`
- **Headline result:** `<a number / concrete outcome>`
- **Demo:** `python src/main.py "<example query>"`

## Source

- **Reference:** `<link or path>`
- **Why this concept:** `<what you want to learn>`

## Goal

What "done" looks like. Be concrete.

## Approach

- [ ] Step 1 —
- [ ] Step 2 —
- [ ] Step 3 —

## Concepts practiced

- [<concept>](../../concepts/<concept>.md)

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Results

See `notes.md` for the running log.
```

### `_template/notes.md`

```markdown
# Notes

Running log. One entry per session. Newest at the top.

---

## YYYY-MM-DD

**What we covered:**

**What worked:**

**What broke:**

**Next:**
```

### `_template/requirements.txt`

```
# Add dependencies as you go
```
