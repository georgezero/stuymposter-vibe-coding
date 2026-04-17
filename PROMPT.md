# Stuymposter — Vibe Coding Starter Prompt

> Paste everything below the horizontal line into your AI coding tool to start building.
> Works with Google Antigravity, Claude Code, or OpenAI Codex.
> The AI will ask you questions along the way — answer them to make it your own.

---

I want to build a web app called **Stuymposter** — a social deduction word game for Stuyvesant High School students.

This is a **pass-and-play** game. Everyone plays on one phone or laptop that gets passed around the table. There is no online multiplayer.

---

### How the game works

**Stuymposter** is based on the Imposter Game — a social deduction word game where most players receive the same secret word, while one player is the **Imposter** and sees something different.

#### Roles

- **Civilians (majority)** — all see the same secret word.
- **The Imposter (one player)** — sees a different related word, or nothing at all.

#### Clue Phase

Players take turns giving **one-word clues** related to their secret word, without saying the word directly.

Example: if the word is **Apple**, civilians might say:
- *fruit*
- *Newton*

The Imposter listens carefully to deduce the real word, then gives a vague or generic clue to avoid suspicion — for example: *edible*.

- **Civilians** try to build a chain of connected clues that signal knowledge of the word.
- A good civilian clue is specific but not obvious — *"phone company"* for Apple is better than *"red fruit"*, because it proves knowledge without handing the Imposter the answer.
- **Imposters** should mimic the style of other clues, avoid over-explaining, and redirect suspicion toward others.

This phase typically lasts **2–3 rounds** of clues.

#### Voting Phase

After the clue rounds:

1. Players discuss who they think the Imposter is.
2. They analyze clues and behavior — looking for vague answers, hesitation, or suspicious patterns.
3. Everyone votes on one player.
4. The player with the most votes is **eliminated** and their role is revealed.

Common mistakes:
- Describing the word too directly (gives the Imposter the answer)
- Voting too early without enough information

#### Win Conditions

- **Civilians win** if they correctly identify and eliminate the Imposter.
- **The Imposter wins** if they survive the vote.
- **If the player chose "Discussion only" (Question 3C):** There is no in-app voting, so there is no winner to declare. The app only reveals who the Imposter was.

---

### Stack

Use this exact stack — don't switch anything out:

- **Runtime**: Node.js with ESM modules (`"type": "module"` in package.json)
- **Language**: TypeScript (not strict mode — use `"strict": false` in tsconfig so beginners don't hit confusing type errors)
- **Web framework**: Hono (`hono` + `@hono/node-server`) — serves both the HTML page and JSON API endpoints
- **Frontend**: Vanilla HTML + CSS + JavaScript — use the browser's built-in `fetch()` API to call the server. No React, no HTMX, no Vue.
- **CSS**: Tailwind CSS (via CDN for simplicity — `<script src="https://cdn.tailwindcss.com"></script>`)
- **ORM**: Drizzle ORM
- **Hot reload**: Use `tsx --watch` for development so code changes appear instantly without restarting

> **Why fetch + vanilla JS?** This is how the web fundamentally works — your frontend sends requests to the server, gets data back, and updates the page. React, Vue, and every other framework build on top of this same idea. Learning it here means everything else will make sense later.

---

### Before writing any code, ask me these four questions one at a time:

---

**Question 1 — Imposter hint**

When the Imposter gets their word screen, should they:

**A) See a related but different word** (e.g. civilians see "BC Calc", Imposter sees "Pre-Calc") — harder for civilians because the Imposter can give convincing clues.

**B) See "???"** — the Imposter has no idea what the word is and must bluff entirely from listening to others. More chaotic and fun.

Which do you prefer? (You can also say "let the host choose before each game".)

---

**Question 2 — Word storage**

**A) Hard-coded in a JSON file** — simpler, no database needed. Words live in a `.json` file you can edit directly.

**B) SQLite database via Turso** — words live in a real database with an admin page to add/edit them. Requires a free Turso account.

Not sure? Go with A — you can always upgrade later.

---

**Question 3 — Rounds**

**A) End after the first vote** — fast, great for a party.

**B) Multiple rounds** — eliminated players are out, game continues until the Imposter is caught or only 2 players remain (Imposter wins).

**C) Discussion only** — Skip in-app voting entirely. After the clue phase, show a discussion screen with a countdown timer, all player names listed, and a "Reveal Imposter" button. Players discuss out loud and tap Reveal when ready. *Since there's no in-app voting, the app cannot determine who won — the Result screen should only reveal who the Imposter was and show everyone's words. Do not show "Civilians Win" or "Imposter Wins".*

---

**Question 4 — Discussion timer**

Should the discussion screen show a countdown timer?

**A) Yes** — Show a visible countdown during the discussion phase. How many minutes? (default: 2 minutes)

**B) No** — No timer; players decide when they're ready to reveal.

*Note: A timer makes most sense with option C above, but works with any round style.*

---

Once I answer, build the full app from scratch in the current folder. After creating each file, explain in 2–3 plain sentences what it does and why it exists — I'm learning as I build.

---

### Architecture

The app has two parts that talk to each other:

**Server (Hono)** — handles all game logic. To survive server restarts, games must be persisted to a `games.json` file. The server must listen on `0.0.0.0` (not `localhost`) so phones on the same WiFi can connect:

```ts
serve({ fetch: app.fetch, port: 3000, hostname: '0.0.0.0' });
```

Log both the local and network URLs on startup so the user knows what to type on their phone:
```ts
import { networkInterfaces } from 'node:os';
const localIP = Object.values(networkInterfaces()).flat()
  .find(i => i?.family === 'IPv4' && !i.internal)?.address ?? 'unknown';
console.log(`Local:   http://localhost:3000`);
console.log(`Network: http://${localIP}:3000  ← open this on your phone`);
```

Exposes a JSON API:

```
POST /api/games                    — create a new game
POST /api/games/:id/players        — add a player
POST /api/games/:id/start          — start game, assign roles
GET  /api/games/:id/state          — get current game state
POST /api/games/:id/reveal         — mark current player's word as revealed
POST /api/games/:id/vote           — cast a vote (not needed for Question 3C)
POST /api/games/:id/finalize       — reveal the imposter and win state
```

> **If Question 3C (Discussion only):** The `/vote` endpoint is not needed. The `/finalize` endpoint should reveal the Imposter's identity but must **not** set or return any win/loss state.

**Frontend (single HTML page)** — one `index.html` served by Hono. Vanilla JavaScript.
- Use `localStorage` to save the `gameId` so refreshes don't lose the game.
- If a `fetch()` returns a 404, the app should "self-heal" by returning home.
- UI must support "Enter" key and autofocus for adding players.

---

### Screens

1. **Home** — App name, tagline, "New Game" button
2. **Player Setup** — Enter names one at a time (3–8 players). Running list shows who's added. "Start Game" button appears once ≥3 players are in.
3. **Word Reveal** (pass-and-play) — Shows "Pass the phone to [Name]". Tap to reveal their word. Use colors to signal roles: **Red border** for Imposter, **Green border** for Civilian. "Done" button only appears after word is shown.
4. **Verbal Clues** — Players discuss clues out loud at the table. The phone can be left on the table or passed around for reference.
5. **Voting/Discussion** — Depends on Question 3:
   - **(A or B) Voting:** Each player taps who they think is the Imposter. One vote per player (pass the phone). Includes a "Reveal Imposter" button to end the game. If a timer was chosen (Question 4A), show the countdown here.
   - **(C) Discussion only:** Show a centered screen with the countdown timer (if chosen), the heading "Who is the Imposter?", a subheading "Discuss clues out loud, then cast your final vote.", all player names listed, and a large "Reveal Imposter" button. No tapping to vote — just discussion and reveal.
6. **Result** — Show who was the Imposter. If Question 3A or B was chosen, show whether Civilians or the Imposter won. If Question 3C was chosen, **do not show a winner** — only reveal the Imposter's identity and show everyone's secret words. Option to play again.

---

### Word Packs

Include these two starter word packs. I'll customize them after — just use these as the starting data.

**Pack 1: Hardest Classes at Stuy**

| Civilian | Imposter |
|---|---|
| BC Calculus | Pre-Calculus |
| AP Physics C | AP Physics 1 |
| Physiology | AP Biology |
| APUSH | AP World History |
| Research (Science) | Independent Study |
| Linear Algebra | Algebra 2 |
| English 11 | English 10 |
| AP Chemistry | Regents Chemistry |
| Multivariable Calc | BC Calculus |
| Stuyvesant Math Team | Math League |

**Pack 2: Stuy Traditions & Culture**

| Civilian | Imposter |
|---|---|
| SING! | School Musical |
| The Spectator | School Newspaper |
| Stuy Oval | Quad |
| The Escalators | The Stairs |
| Arista | Honor Society |
| BigSIB | Orientation |
| Stuyvesant Beacon | School Website |
| The 1 Train | The Subway |
| Senior Lounge | Common Room |
| Bridge Day | Class Trip |

---

### Design system

Use this exact design system — it's been tested and looks great on phones in dim rooms:

```html
<!-- In <head> — load Outfit font and set base styles -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;700;900&display=swap" rel="stylesheet">
<style>
  body { font-family: 'Outfit', sans-serif; background: #0f172a; color: #f8fafc; }
  .card { background: #1e293b; border: 1px solid #334155; }
  .btn-primary { background: #6366f1; transition: all 0.2s; }
  .btn-primary:hover { background: #4f46e5; transform: translateY(-2px); }
</style>
```

- **Background:** `#0f172a` (deep navy/slate)
- **Cards:** `#1e293b` with `border: 1px solid #334155`
- **Primary accent:** Indigo — `#6366f1` buttons, `text-indigo-400` highlights
- **Secondary text:** `text-slate-400`
- **Font:** Outfit — use `font-black` for headings, `font-bold` for buttons, regular for body
- **Timers:** `font-mono` in `text-indigo-400`; pulse red (`text-rose-500 animate-pulse`) under 30 seconds, bounce red (`text-rose-600 animate-bounce`) at 0:00
- **Cards:** `rounded-3xl p-8` — generous padding, very rounded corners
- **Buttons:** `w-full py-4 rounded-2xl font-bold text-lg` — always full-width, large tap targets
- **Transitions:** Use `hidden` / `block` toggling with a CSS `opacity` fade for screen changes

Apply this design system from the very first file. Do not use a plain white background or default browser styles.

---

### UI requirements

- Mobile-first. All buttons must be large enough to tap on an iPhone without zooming.
- No login, no accounts.
- Each screen should feel like a card — centered, clean, readable in a dim room.
- Neutral card colors — never use red or any color that hints at someone being the Imposter before the role is revealed.
- The app should work fully offline after the first page load (except Tailwind CDN).

---

### Project setup (do this first, before any app code)

1. Run `git init` and create a `.gitignore` that excludes `node_modules/`, `.env`, and `dist/`
2. Create a `.env.example` file — even if it's empty for now, every real project uses environment variables for secrets like API keys and database passwords. Add a comment explaining this.
3. Create `package.json` with `"type": "module"` and a `dev` script using `tsx --watch src/index.ts`
4. After the app is working, make a first git commit with message: `feat: initial working Stuymposter`

---

### Local dev instructions

After building, give me step-by-step instructions to:

1. **Automated Node Setup (do this before anything else):**
   - First, check if `node` is already available by running `node --version`.
   - If that fails, **do not stop** — check these common install locations before declaring it missing:
     - `/opt/homebrew/bin/node` (Homebrew on Apple Silicon Mac)
     - `/usr/local/bin/node` (Homebrew on Intel Mac)
     - `~/.nvm/versions/node/*/bin/node` (nvm)
     - `~/.volta/bin/node` (Volta)
   - If found at a non-PATH location, run it directly using the full path (e.g., `/opt/homebrew/bin/node`) and add the directory to PATH for the session: `export PATH="/opt/homebrew/bin:$PATH"`.
   - If `node` is truly not installed anywhere, install it immediately: `brew install node` on Mac (or `winget install OpenJS.NodeJS` on Windows). Do not ask the user to do this — just do it.
   - After confirming node is available, run `npm install` using the same resolved path.
2. Run `npm install`
3. Start the dev server with `npm run dev`
4. Open it on my phone over the same WiFi (using the laptop's local IP address)

---

### Stretch goals (only build if I ask)

- Admin page to add/edit word packs
- Vercel deployment so friends can play from anywhere
- QR code on the home screen
- Score tracking across multiple games in a session
- Authentication (so players have accounts and game history is saved)

> **Note on future projects:** Once you've built this, the same pattern — Hono routes, Drizzle, TypeScript, fetch on the frontend — is the foundation for almost any web app. Your next project might add React on the frontend instead of vanilla JS, or swap SQLite for Postgres, or add authentication. But the core idea is the same.

---

### Skills (optional — use after the app is working)

This repo includes skills in `.agent/skills/`. Once your app is running, you can trigger them by just describing what you want:

- **"Make the app look better"** → frontend skill (UI redesign with Tailwind)
- **"Add a word pack about [topic]"** → add-pack skill (guided word pair creation)
- **"Deploy it so my friends can play"** → deploy skill (Vercel step-by-step)
- **"What does this code do?"** → explain skill (plain-English breakdown)
- **"I'm getting an error"** → debug skill (root cause diagnosis and fix)

See `SKILLS.md` for the full list and how to write your own.

---

Build it. Ask me the four questions first, then start.
