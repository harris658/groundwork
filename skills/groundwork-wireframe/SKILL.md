---
name: groundwork-wireframe
description: Draw a hand-drawn Excalidraw concept diagram after a learning step lands. Use this when a concept is confirmed working (the learner has seen real output), a chapter is complete, or the user says "draw a diagram", "wireframe this", "draw the architecture", or "visualise this". A diagram is a recall aid — it makes the concept stick and gives something to look back at.
---

# Groundwork: Wireframe

A hand-drawn diagram is one of the best ways to make a concept stick and to recollect it later. Draw one whenever a concept — or a whole chapter — is confirmed working.

## Protocol

Run these steps in order. Do not skip step 1.

1. **Call `mcp__claude_ai_Excalidraw__read_me`** — always, every time, before anything else. This returns the current element format. The format changes; always read it fresh.
2. **Call `mcp__claude_ai_Excalidraw__create_view`** with a diagram covering:
   - The key concept(s) just covered
   - How data flows through the system
   - Where this piece fits in the overall system (show its place in the chain)
3. **Call `mcp__claude_ai_Excalidraw__export_to_excalidraw`** to get a shareable URL.
4. **Save the URL** in the relevant `notes.md` under a `## Diagram` heading, then commit.

## Style rules

- Hand-drawn feel — Excalidraw default strokes, not clean corporate lines.
- Flow left → right or top → bottom. Label every arrow.
- Highlight where the current concept "lives" in the broader system.
- Readable at a glance — this is a recall aid, not a textbook figure.
- Keep it sparse: one main concept, its inputs, its outputs, and where it sits in the chain. Don't draw the whole system every time.
