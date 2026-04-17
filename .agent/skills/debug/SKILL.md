---
name: debug
description: Use this skill when the user has an error, something is broken, the app crashes, a page shows blank, a button doesn't work, the terminal shows a red error message, or anything is not behaving as expected.
---

# Debug

## Goal
Find the root cause of the problem, explain it in plain English, and fix it — without making unrelated changes to the code.

## Instructions

1. **Get the full error** — ask if they haven't already provided it:
   > "Can you paste the exact error message? If it's in the terminal, copy all the red text. If it's in the browser, open DevTools (F12), go to the Console tab, and paste what you see."

2. **Read the error carefully before doing anything.** Identify:
   - What file and line number is mentioned?
   - What type of error is it? (syntax error, cannot find module, undefined, network error, etc.)
   - Is this a server error (terminal) or a browser error (console)?

3. **State the diagnosis in plain English** before touching any code:
   > "The problem is: [plain English explanation]. This is happening because: [cause]."
   
   Common causes to check first:
   - `Cannot find module` → missing `npm install` or wrong import path
   - `undefined is not a function` → variable is null/undefined before being used
   - `fetch failed` or `404` → the URL the frontend is calling doesn't match the route on the server
   - `SyntaxError` → a missing bracket, comma, or quote somewhere
   - `EADDRINUSE` → another process is already running on that port — kill it with `npx kill-port 3000`
   - TypeScript red underlines → type mismatch, usually safe to ignore in dev but worth fixing

4. **Make the minimal fix** — change only what's necessary to fix this specific error. Don't refactor or improve nearby code.

5. **Explain the fix** in one sentence:
   > "I changed X in file Y because Z."

6. **Verify it's fixed** — tell the user exactly what to do to confirm:
   > "Save the file, then check if [specific thing] works now."

## Constraints
- Fix one error at a time
- Do not make improvements or refactors while fixing a bug
- If you're not sure what the cause is, say so — then ask for more information rather than guessing
- Do not delete code unless you're certain it's the cause of the problem

## If stuck
If the error is unclear after reading it, ask:
> "What were you doing right before this error appeared? Did it ever work before?"
The answer almost always points to what changed.
