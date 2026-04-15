# MiaoLog — Worked Example Spec

MiaoLog (喵Log) is the worked example used throughout ENT208TC.
This folder shows what a complete `spec/` folder looks like for a real product.

Use it as a template. Replace MiaoLog's content with your own product.

## Files in this folder

| File | What it is |
|---|---|
| `product.md` | One-paragraph overview: what it does, who uses it, key constraints |
| `prd.md` | Product Requirements Document: problem, requirements, out of scope |
| `roles.md` | User role definitions: who can do what, permission rules for the AI agent |
| `user-stories.md` | Detailed user stories with acceptance criteria |
| `stack.md` | The tools the team chose and the reason for each choice |
| `ui-spec.md` | Design system: colours, fonts, screen layouts, interaction patterns |

## How to use this with an AI coding agent

Start each AI session with:

> "Read the files in my spec/ folder. Then help me build: [user story from user-stories.md]."

The agent reads your product overview, requirements, user roles, acceptance criteria,
stack, and design — all at once. You do not need to paste context into every prompt.

## What this folder is NOT

- Not a complete codebase (no code files here — spec only)
- Not a final document — update it as you build and learn
- Not a report — it is a working reference for your team and your AI agent
