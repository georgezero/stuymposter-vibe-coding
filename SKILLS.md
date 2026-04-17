# Skills

Skills are modular AI instructions that live in this repo. When you describe a task in Google Antigravity, it automatically loads the right skill for the job — you don't have to invoke them manually.

---

## What is a skill?

Think of skills as specialized modes for the AI. Instead of one giant prompt that covers everything, skills are focused instruction sets that only activate when relevant.

This means:
- The AI stays fast and accurate — it only loads what it needs
- You can add new skills without changing the base app
- Skills are version-controlled — your teammates get them automatically when they clone the repo

---

## Available skills

| Skill | When it activates |
|---|---|
| `frontend` | "Make it look better", "improve the UI", "add colors", "it looks bad on my phone" |
| `add-pack` | "Add a new word pack", "I want to make one about teachers", "add more words" |
| `deploy` | "Put it on the internet", "how do I share this", "deploy to Vercel", "get a public URL" |
| `explain` | "What does this do?", "explain this file", "I don't understand X", "what is a route?" |
| `debug` | "It's broken", "I'm getting an error", "the button doesn't work", "blank screen" |

---

## How to use a skill

Just describe what you want in plain English. Your tool routes to the right skill automatically.

Examples:
- *"I want to make the app look more like a real game — dark theme, big buttons"* → activates `frontend`
- *"Can you add a word pack about NYC foods?"* → activates `add-pack`
- *"I got a red error in the terminal, not sure what it means"* → activates `debug`
- *"What does `async/await` mean?"* → activates `explain`

### How routing works per tool

| Tool | How skills are discovered |
|---|---|
| **Google Antigravity** | Reads `.agent/skills/` natively — semantic matching is automatic |
| **Claude Code** | Reads `CLAUDE.md` on startup — routing rules there point to the skill files |
| **OpenAI Codex** | Reads `AGENTS.md` on startup — same routing rules, same skill files |

All three tools use the same skill files in `.agent/skills/`. Only the discovery mechanism differs.

---

## Where skills live

```
.agent/
  skills/
    frontend/     — UI redesign
    add-pack/     — create new word packs
    deploy/       — Vercel deployment
    explain/      — plain-English explanations
    debug/        — error diagnosis and fixes
```

Each skill is a folder with a `SKILL.md` file inside. You can open any of them to see exactly what instructions the AI follows — no magic, just text.

---

## Creating your own skill

Once you're comfortable, try writing your own. Create a new folder under `.agent/skills/` with a `SKILL.md` file:

```
.agent/skills/my-skill/SKILL.md
```

The file needs two parts:

**1. YAML frontmatter** — tells Google Antigravity when to activate the skill:
```yaml
---
name: my-skill
description: Use this skill when the user wants to [very specific description of when this applies].
---
```

**2. Markdown body** — the actual instructions for the AI:
```markdown
## Goal
What this skill achieves.

## Instructions
1. Step one
2. Step two

## Constraints
- What NOT to do
```

The `description` field is the most important part — be specific. "Helps with code" won't work. "Use this skill when the user wants to add a new game mode with a timer for the clue phase" will.
