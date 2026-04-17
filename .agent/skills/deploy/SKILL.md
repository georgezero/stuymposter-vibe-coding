---
name: deploy
description: Use this skill when the user wants to deploy the app, put it on the internet, share it with friends, get a public URL, or publish to Vercel. Also use when the user asks how to make the app accessible outside their local WiFi network.
---

# Deploy to Vercel

## Goal
Deploy the app to Vercel so it has a public URL that anyone can open — no laptop required.

## Instructions

1. **Check prerequisites** — before doing anything, ask:
   > "Have you signed up for a free Vercel account at vercel.com? (yes / not yet)"
   If not yet: tell them to go to vercel.com, sign up with GitHub, and come back.

2. **Check the current build** — make sure the app runs locally first:
   > "Run `npm run dev` — does the app open in your browser without errors? (yes / no)"
   If no: stop and fix the local errors first before deploying.

3. **Explain what Vercel is** in one sentence before proceeding:
   > "Vercel is a free hosting service. It takes your code, builds it, and gives you a URL like `stuymposter-yourname.vercel.app` that anyone can open."

4. **Create a Vercel config file** — add `vercel.json` to the project root:
   ```json
   {
     "version": 2,
     "builds": [{ "src": "src/index.ts", "use": "@vercel/node" }],
     "routes": [{ "src": "/(.*)", "dest": "src/index.ts" }]
   }
   ```

5. **Add a build script** — make sure `package.json` has:
   ```json
   "scripts": {
     "dev": "tsx --watch src/index.ts",
     "build": "tsc",
     "start": "node dist/index.js"
   }
   ```

6. **Handle the database** — ask:
   > "Are you using a JSON file for word packs, or Turso/SQLite?"
   - If JSON: no extra steps needed.
   - If Turso: they need to add their `DATABASE_URL` and `DATABASE_AUTH_TOKEN` as environment variables in the Vercel dashboard. Explain how to do this step by step.

7. **Install Vercel CLI and deploy:**
   ```bash
   npm install -g vercel
   vercel
   ```
   Walk them through each prompt from the CLI output.

8. **Test the deployed URL** — once deployed, open the URL and verify:
   - Home screen loads
   - Can start a new game
   - Word reveal works

9. **Commit the new files:**
   ```bash
   git add vercel.json package.json
   git commit -m "feat: add Vercel deployment config"
   ```

## Constraints
- Do not store secrets (API keys, database tokens) in code files — only in Vercel environment variables
- If the app uses a local SQLite file (`file:./...`), it will not work on Vercel — the user must switch to Turso for cloud deployment

## After deployment
Tell the user:
> "Your app is live. Share the URL and anyone can play — no laptop needed. Every time you push a new commit to GitHub, Vercel will automatically redeploy."
