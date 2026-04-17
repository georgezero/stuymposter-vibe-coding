---
name: frontend
description: Use this skill when the user wants to improve the UI, redesign how the app looks, make it more polished or visually appealing, fix layout issues on mobile, add colors or animations, or generally make the frontend look better. Do not use for game logic changes.
---

# Frontend Polish

## Goal
Audit the current UI and make it look significantly better using Tailwind CSS — without touching any game logic or API code.

## Instructions

1. **Read the current frontend** — open `src/index.html` (or wherever the HTML lives) and the CSS. Note what's working and what looks rough.

2. **Ask one question before doing anything:**
   > "What's the vibe you're going for? (e.g. dark and mysterious, clean and minimal, bright and fun, Stuy school colors navy/gold)"
   Wait for their answer.

3. **Audit the current UI against these criteria:**
   - Are buttons large enough to tap on a phone? (min height 48px)
   - Is text readable in a dim room? (sufficient contrast)
   - Does it feel like a game, or a form?
   - Is the layout centered and card-based?
   - Are there any colors that give away player roles before the reveal?

4. **Propose 3 specific improvements** before making any changes. Number them. Wait for approval or ask which ones to do.

5. **Implement the approved changes** using Tailwind utility classes. Prioritize:
   - Typography: font size, weight, line height
   - Spacing: padding, margins, gap
   - Color: backgrounds, text, borders — themed to their answer from step 2
   - Motion: subtle fade or slide transitions between screens (CSS only, no JS libraries)
   - Mobile feel: full-width buttons, touch-friendly tap targets

## Constraints
- Do not change any JavaScript game logic
- Do not change any Hono route handlers
- Do not change JSON data or word packs
- Do not add new npm packages — Tailwind CDN is already loaded
- Keep all cards neutral-colored until a role is revealed

## Example output
After making changes, show a before/after summary:
```
Changed:
- Home screen: dark navy background, gold "STUYMPOSTER" heading, larger New Game button
- Word reveal card: neutral dark slate (was white), larger tap target
- Voting buttons: full-width, spaced out, clear active state
```
