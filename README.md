# Stuymposter — Vibe Coding Project

A social deduction word game for Stuyvesant High School students, built with AI.

This repo is a **starter kit for a vibe coding exercise**. You paste the prompt into an AI coding tool, answer a few design questions, and the AI builds you a working app.

---

## What you're building

A pass-and-play version of the Imposter Game, Stuy-themed. One phone, 3–8 players, passed around the table. Players give clues about a secret word while one player (the Imposter) tries to blend in without knowing the real word.

<img width="1493" height="844" alt="image" src="https://github.com/user-attachments/assets/1e5d0fd1-5562-47c2-8a37-a8f719a7df15" />


---

## How to use this repo

### 1. Open `PROMPT.md`

That's the prompt. Copy everything below the horizontal line and paste it into your AI coding tool — Google Antigravity, Claude Code, or OpenAI Codex all work.

### 2. Answer the four design questions

The AI will ask you:
- Should the Imposter see a hint word or nothing?
- Hard-coded JSON word packs or a real database?
- One round, multiple elimination rounds, or discussion-only (no in-app voting)?
- Should there be a countdown timer during the discussion phase?

Answer each one. Your answers shape what gets built.

### 3. Let it build

The AI creates every file from scratch and explains what each one does. When it's done, run:

```bash
npm install
npm run dev
```

Open your browser to `http://localhost:3000`. The server also prints a **Network** URL in the terminal — use that to connect from your phone.

### 4. Open it on your phone

Open the Network URL printed in the terminal (e.g. `http://192.168.x.x:3000`) on your phone. The server listens on all interfaces so any device on the same WiFi can connect. Pass it around and play.

### 5. Make it yours

Edit `word-packs/` to add your own words. Add a new pack about your friend group, your neighborhood, your favorite shows — whatever makes it yours.

---

## Repo contents

```
PROMPT.md          — the starter prompt (works with Google Antigravity, Claude Code, Codex)
CLAUDE.md          — project instructions + skill routing for Claude Code
AGENTS.md          — project instructions + skill routing for OpenAI Codex
SKILLS.md          — what skills are and how to use them
TEACHER.md         — class structure, discussion questions, stuck-point guide
word-packs/
  hardest-classes.json   — starter pack: hardest Stuy classes
  stuy-culture.json      — starter pack: Stuy traditions & culture
  README.md              — how to create your own word packs
.agent/skills/
  frontend/        — redesign the UI (Tailwind, colors, mobile polish)
  add-pack/        — create a new themed word pack
  deploy/          — deploy to Vercel step by step
  explain/         — explain any file or concept in plain English
  debug/           — diagnose and fix errors
```

Your actual app code will be created by the AI in this folder when you run the prompt.

---

## Stack

| Layer | Tool |
|---|---|
| Server | Hono + Node.js |
| Language | TypeScript |
| Frontend | Vanilla JS + fetch() |
| CSS | Tailwind CSS |
| Database | JSON file or Turso (SQLite) |
| ORM | Drizzle (if using DB) |
| Deploy | Vercel (stretch goal) |

---

## After this project

The same stack — Hono routes, Drizzle, TypeScript, fetch on the frontend — is the foundation for almost any web app. Your next project might add React on the frontend, swap SQLite for Postgres, or add user authentication. The core idea is the same: a server handles logic and data, a frontend shows it to users.

---

### Screenshots

<img width="1501" height="851" alt="image" src="https://github.com/user-attachments/assets/b3aa5bf7-7dfa-4202-b0a8-d265c9582792" />

<img width="1495" height="844" alt="image" src="https://github.com/user-attachments/assets/4597f475-3df0-4a6f-8228-74491abdb977" />

<img width="1491" height="841" alt="image" src="https://github.com/user-attachments/assets/7005bbf5-f5f1-4461-9836-5752b88ea518" />

<img width="1501" height="844" alt="image" src="https://github.com/user-attachments/assets/19505b88-ac6a-4588-93e2-7b83d69bd689" />



<img width="1502" height="850" alt="image" src="https://github.com/user-attachments/assets/7805ecf6-e2ce-4aab-aa09-8498fab1c627" />

<img width="1502" height="845" alt="image" src="https://github.com/user-attachments/assets/be132aa3-4ffd-4cce-8d67-cdfcddf7a564" />

<img width="1500" height="841" alt="image" src="https://github.com/user-attachments/assets/b64d476c-98a3-42a5-a148-0e10636ef3c7" />

<img width="1501" height="846" alt="image" src="https://github.com/user-attachments/assets/e0c1834e-548c-4152-978e-0800cfb48e93" />




