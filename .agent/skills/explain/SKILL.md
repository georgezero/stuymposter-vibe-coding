---
name: explain
description: Use this skill when the user asks what a file does, how something works, what a word means (like API, route, fetch, async, JSON, TypeScript), or wants to understand the code that was generated. Also use when the user seems confused or lost about what was built.
---

# Explain

## Goal
Explain any part of the codebase in plain English that a beginner can follow — no assumed knowledge, no jargon without definition.

## Instructions

1. **Identify what to explain** — if the user didn't specify, ask:
   > "What would you like me to explain? You can paste code, name a file, or just describe what you're confused about."

2. **Start with the real-world analogy** before the technical explanation. Examples:
   - A **route** is like a menu item at a restaurant — when someone orders it (requests a URL), the kitchen (server) prepares a response.
   - **JSON** is like a labeled box — it stores information with names attached, so you know what each piece is.
   - **`fetch()`** is like a text message — your browser sends a request to the server and waits for a reply.
   - **TypeScript** is like a recipe with strict measurements — it checks your work before you cook to catch mistakes early.
   - **`async/await`** is like ordering food — you place the order (async call) and go do other things, then come back when it's ready (await).

3. **Explain the specific thing** they asked about in 3–5 sentences. Name the exact file and line number if relevant.

4. **Show where it fits in the bigger picture** — one sentence on how this piece connects to the rest of the app.

5. **End with a check-in:**
   > "Does that make sense? Want me to go deeper on any part?"

## Constraints
- No jargon without an immediate plain-English definition
- If explaining a function, say what goes IN and what comes OUT before explaining the internals
- Never say "it's just" or "simply" — it minimizes the learner's confusion and isn't helpful
- Keep explanations short — 5 sentences max per concept, then check in before continuing

## Example

**User:** "What does this do: `app.get('/api/games/:id/state', async (c) => {`"

**Response:**
> This is a **route** — it tells the server: "when someone visits the URL `/api/games/[some-id]/state`, run this code."
>
> The `:id` part is a placeholder — like a blank in a form. If the URL is `/api/games/42/state`, then `id` equals `42` inside the function.
>
> The `async` keyword means this function might need to wait for something (like reading from the database) before it can respond. The `c` is a shorthand for "context" — it holds the request and lets you send back a response.
>
> In the bigger picture: this is the main endpoint your frontend calls every time it needs to know what screen to show the player.
