# Groundwork

> A Claude Code plugin for deep, concept-by-concept learning. Theory before practice. One idea at a time. Depth over speed.

Most AI-assisted learning goes wrong the same way: you ask a question, Claude gives you a wall of text, you run some code, and two hours later you couldn't explain what you built. Groundwork is a structured protocol that prevents this — every session has a theory half before a practice half, every concept is taught from a declared source, and every session ends with a written checkpoint so the next one can pick up exactly where you left off.

## Install

```bash
npx skills add harris658/groundwork --agent claude-code
```

Restart Claude Code after installing. The four `groundwork:*` skills will appear automatically.

## Quick start

```
you:   groundwork setup
```

Groundwork asks where to create your workspace and what to call it, then scaffolds the full directory structure. Open the workspace in Claude Code and you're ready.

```
you:   let's learn about transformer attention
```

`groundwork:teach` fires automatically. It asks for your reference source, teaches the concept from scratch, then walks you through a hands-on step — theory first, code second.

## Skills

### `groundwork:teach`
The core skill. Fires whenever you want to learn something.

**What it does:**
- Asks for your reference source before teaching anything (a video, paper, wiki, transcript — anything). Teaches from that, not from general knowledge.
- Explains the *problem* a concept solves before explaining the concept itself.
- One concept per message, then stops. No walls of text.
- Gives the mental model + a real-world analogy + names the common misconception.
- Writes code for you, gives you exact commands to run, waits for your output before debriefing.
- After you run it: structured debrief — what we built, pros, cons, why move on.
- Never says "obviously", "simply", or "just". Never pushes you to write code yourself.

**Triggers on:** "teach me X", "let's learn X", "explain X", "walk me through X", "step N of Y", continuing any learning session.

---

### `groundwork:resume`
Handles session continuity across conversations.

Claude has no memory between conversations. The only thing that persists is what's on disk. This skill keeps the trail complete enough to resume cold — every time.

**On pause** ("I'm stopping", "let's continue later"):
1. Writes a `notes.md` entry with a concrete `Next:` line
2. Commits everything — the git log is the learning record
3. Flags anything worth capturing in the concept library

**On resume** ("resume", "continue [project]", "where did we leave off?"):
1. Reads `notes.md`, the README checklist, and `git log`
2. Summarises in 2–3 lines: last step done, what broke, what's next
3. Confirms with you before writing any new code

**Triggers on:** "pause", "I'm stopping", "resume", "continue [project]", "where did we leave off?"

---

### `groundwork:wireframe`
Draws a hand-drawn Excalidraw diagram after a concept lands.

A diagram forces you to recall the structure, not just recognise it. After each concept is confirmed working, this skill draws a flow diagram showing the key concepts, how data moves through the system, and where this piece fits in the broader chain.

Saves the shareable URL to `notes.md` and commits it.

**Requires:** the [Excalidraw MCP](https://github.com/claude-ai/excalidraw-mcp) to be configured.

**Triggers on:** concept confirmed working, chapter complete, "draw a diagram", "wireframe this."

---

### `groundwork:setup`
Scaffolds a complete learning workspace from scratch.

Run this once in a new directory. It creates everything you need to start learning concept-by-concept — including a `CLAUDE.md` already wired to the Groundwork skills.

**What it creates:**

```
my-workspace/
├── CLAUDE.md               # workspace config — wires groundwork skills, reference sources
├── README.md               # portfolio hub with project table and learning tracks
├── .gitignore              # ignores .env, data/, projects/
├── .env.example            # API key template
├── concepts/               # durable theory library — one note per concept
│   ├── README.md           # concept index
│   └── _template.md        # skeleton for a new concept note
├── _template/              # copy this to projects/<name> for each new project
│   ├── README.md           # project README with Showcase, Source, Goal, Approach
│   ├── notes.md            # session log template
│   ├── requirements.txt
│   ├── src/
│   └── data/
├── docs/                   # specs and design docs
├── data/                   # shared corpora reused across projects
└── projects/               # individual project repos (each is its own git repo)
```

**Triggers on:** "groundwork setup", "set up a learning workspace", "initialize a groundwork workspace."

## How a session works

1. **Start** — say what you want to learn. `groundwork:teach` asks for the reference source.
2. **Theory** — Claude explains the concept: problem first, then what it is, analogy, misconception. Stops after one idea.
3. **Practice** — Claude writes the code, gives you exact commands. You run them, paste back the output.
4. **Debrief** — after you've seen real output, Claude explains what you built, what it can't do, and why the next step matters.
5. **Pause** — say "I'm stopping." `groundwork:resume` writes the checkpoint and commits.
6. **Resume** — next session, say "resume [project]." `groundwork:resume` reads the trail and picks up exactly where you left off.

## Philosophy

**The learner owns the concepts, not the syntax.** You run every terminal command. Claude writes every line of code. The goal is for you to be able to explain what you built and why it works — not to produce the syntax yourself.

**A clarifying question means the explanation wasn't complete.** It's the teacher's cue to go deeper, not the learner's failure.

**The git log is the learning record.** Commit after every working step. Push after every commit. If it isn't committed, it didn't happen.

**Never end a session with unwritten learning.** A new conversation has no memory of the previous one. Only the files persist.

## License

MIT
