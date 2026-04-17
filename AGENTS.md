# Stuymposter — Project Instructions

## What this is

A pass-and-play social deduction word game for Stuyvesant High School students. One device, 3–8 players, passed around the table. Built as a vibe coding teaching project.

## Stack

- **Server**: Hono + Node.js (ESM, `"type": "module"`)
- **Language**: TypeScript (`"strict": false`)
- **Frontend**: Vanilla HTML + CSS + JavaScript (`fetch()` API, no React, no HTMX)
- **CSS**: Tailwind CSS via CDN
- **ORM**: Drizzle ORM
- **DB**: JSON file (default) or Turso/SQLite
- **Hot reload**: `tsx --watch`

## Project structure (once built)

```
src/
  index.ts       — Hono server, mounts all routes
  routes/        — API route handlers (return JSON)
  db/            — Drizzle schema and client
public/
  index.html     — Single HTML page, vanilla JS frontend
word-packs/      — JSON word pair data
.agent/skills/   — AI skills (see skill routing below)
```

## Skill routing

When the user's request matches a skill below, read the corresponding SKILL.md and follow its instructions exactly before doing anything else.

| User says something like... | Read this skill |
|---|---|
| "make it look better", "improve the UI", "redesign", "it looks bad on my phone" | `.agent/skills/frontend/SKILL.md` |
| "add a word pack", "new category", "add more words", "I want words about X" | `.agent/skills/add-pack/SKILL.md` |
| "deploy", "put it online", "share with friends", "Vercel", "public URL" | `.agent/skills/deploy/SKILL.md` |
| "what does this do", "explain", "I don't understand", "what is X" | `.agent/skills/explain/SKILL.md` |
| "error", "broken", "not working", "blank screen", "crash", "it's not doing X" | `.agent/skills/debug/SKILL.md` |

## General guidelines

- This is a teaching project. When building or explaining, use plain English. Name the file and line number when relevant.
- After each major file is created, give a 2–3 sentence plain-English summary of what it does.
- Make the minimal change needed. Don't refactor or improve code the user didn't ask about.
- Mobile-first. All tap targets must be large enough for a phone.
- Never use colors that hint at a player's role before it's revealed.
