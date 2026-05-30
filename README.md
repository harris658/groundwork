# Groundwork

A Claude Code plugin for concept-by-concept learning. Theory before practice. Depth over speed.

## Install

```bash
npx skills add harris658/groundwork --agent claude-code
```

## Skills

| Skill | When to use |
|-------|------------|
| `groundwork:teach` | Any learning session — "teach me X", "let's learn X", "explain X" |
| `groundwork:resume` | "pause", "I'm stopping", "resume", "where did we leave off?" |
| `groundwork:wireframe` | After a concept lands — draws an Excalidraw diagram as a recall aid |
| `groundwork:setup` | "groundwork setup" — scaffolds a full learning workspace from scratch |

## What it does

**`groundwork:teach`** enforces a world-class teaching protocol on every session:
- Establishes a reference source before teaching anything
- Theory half before practice half — always
- One concept per message, then stops
- Why before what, real-world analogies, common misconception named
- Debrief after every step: what we built, pros, cons, why move on
- Learner runs every command; teacher writes every line of code

**`groundwork:resume`** handles session continuity:
- On pause: writes `notes.md` with a `Next:` line and commits
- On resume: reads `notes.md` + `git log`, summarises in 2–3 lines, confirms before coding

**`groundwork:wireframe`** draws a hand-drawn Excalidraw diagram after each concept is confirmed working — a recall aid, not a textbook figure.

**`groundwork:setup`** scaffolds a complete workspace:
```
my-learning/
├── CLAUDE.md          # wires in the groundwork skills
├── README.md          # portfolio hub with project table
├── concepts/          # durable theory library
│   ├── README.md
│   └── _template.md
├── _template/         # copy this for each new project
├── docs/
├── data/
└── projects/          # each project is its own git repo
```

## Philosophy

Learning spans many sessions. A new conversation has no memory of the previous one — continuity comes from the trail on disk: `git log`, `notes.md`, the README checklist. Groundwork keeps that trail complete so every session can resume cold without re-doing work.

The learner owns the concepts and directs the build. The teacher writes the code and explains every line. The git log is the learning record.
