# Teacher Guide — Stuymposter Vibe Coding Workshop

## Overview

Students use an AI coding tool (Google Antigravity) to build a working web app from a single prompt. The project is intentionally open-ended — every student's version will look different depending on the choices they make.

The goal isn't to produce identical apps. It's to experience the full loop: idea → prompt → working product → show it to real people.

---

## Session Structure

### Day 1 — Intro (in class, ~30 min)

1. **Play a round of the real Imposter game** (or Stuymposter if already built) so students understand what they're building. 10 min.

2. **Show them the prompt.** Walk through it section by section:
   - What the stack is (don't go deep — just name it)
   - The three design questions they'll answer
   - What the AI will build for them

3. **Demo one question-answer cycle** with Google Antigravity so they see how it works.

4. **Assign homework**: Build their version. They should:
   - Get it running locally on their laptop
   - Customize at least one word pack with their own words
   - Be able to open it on their phone over WiFi and pass it around

---

### Day 2 — Show & Tell (in class)

1. **Each student demos their version** (2–3 min each). They should show:
   - Something that works
   - One choice they made that's different from others
   - One thing they got stuck on and how they got unstuck

2. **Discussion** (see questions below)

3. **Optional**: pair students up to play each other's versions

---

## Discussion Questions (Day 2)

**On the process:**
- What was the first thing you typed and what did the AI do?
- What happened when the AI made a mistake? How did you fix it?
- Did you understand the code it wrote, or did it feel like a black box?
- What would you change about your prompt if you started over?

**On the stack:**
- Your app has a "server" and a "frontend" — what does each one do?
- What is an API endpoint? Can you show me one in your code?
- What does `fetch()` do? Where does the data come from?
- What's in the `.env.example` file? Why does every real project have one?

**On going further:**
- What would you add to this app if you had another day?
- What's a completely different app you could build using the same stack?
- What would change if you added user accounts?

---

## What Students Learn

By building Stuymposter, students touch:

| Concept | Where they see it |
|---|---|
| Client/server model | Frontend fetch → Hono API |
| HTTP requests (GET, POST) | API endpoints |
| JSON data format | Word packs, API responses |
| TypeScript/JavaScript | All code |
| SQL basics (if Turso option) | Drizzle queries |
| Environment variables | `.env.example` |
| Git + version control | Initial commit, git log |
| Deployment | Vercel stretch goal |

---

## Common Stuck Points

**"The AI wrote a lot of code and I don't know what to do"**
→ Tell them to run `npm install` then `npm run dev` first. Get it working before reading the code.

**"I'm getting errors in the terminal"**
→ Copy the exact error message and paste it back into Google Antigravity. Ask it to fix the error.

**"It works on my laptop but not on my phone"**
→ Check they're using the laptop's local IP (e.g. `192.168.x.x:3000`), not `localhost`. Run `ipconfig` (Windows) or `ifconfig` (Mac/Linux) to find the IP.

**"The AI keeps switching my stack / adding React"**
→ Remind them to paste the original prompt again, or tell the AI explicitly: "do not add React, use vanilla fetch only".

**"I chose Turso and can't figure out the database setup"**
→ Have them switch to JSON file storage. It's a 10-minute rebuild and removes the friction.

---

## Stretch Goals for Advanced Students

- Deploy to Vercel and share the URL
- Add a QR code so anyone on their phone can join
- Add a second word pack on a topic they care about
- Add a timer for the clue phase
- Research what "authentication" means and what they'd need to add it
