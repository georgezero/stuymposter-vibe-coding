---
name: add-pack
description: Use this skill when the user wants to add a new word pack, create new word pairs, add a new category of words, or customize the game with their own theme. Also use when the user says they want to make the game about a specific topic.
---

# Add Word Pack

## Goal
Help the user create a new themed word pack and wire it into the game.

## Instructions

1. **Ask for the theme:**
   > "What's the theme for your new pack? (e.g. Stuy teachers, NYC foods, your friend group, a TV show, sports teams)"
   Wait for their answer.

2. **Explain the pair structure** before generating anything:
   > "Each pair has a **civilian word** and an **imposter word**. The civilian word is what most players see — it should be specific and recognizable to your group. The imposter word should be close enough that the imposter can bluff, but different enough that a real civilian would know the difference."
   >
   > Example: Civilian = "BC Calculus", Imposter = "Pre-Calculus"

3. **Generate 10 word pairs** for their theme. Show them as a table:
   | Civilian | Imposter |
   |---|---|
   | ... | ... |

4. **Ask for feedback:**
   > "Does this look right? Tell me any pairs you want to change, remove, or add — or say 'looks good' to continue."
   Wait for their answer. Revise if needed.

5. **Create the JSON file** in `word-packs/` using this format from `references/pack-format.json`. Name the file using the theme (e.g. `word-packs/stuy-teachers.json`).

6. **Wire it into the app** — find where word packs are loaded (likely in `src/index.ts` or a data file) and add the new pack so it appears as an option when starting a game.

7. **Confirm it works** — tell the user to start a new game and verify the new pack appears in the pack selector.

## Constraints
- Only create `.json` files in the `word-packs/` directory
- Do not modify existing word packs
- Civilian and imposter words should be genuinely different — not synonyms

## References
See `references/pack-format.json` for the exact JSON structure to use.
