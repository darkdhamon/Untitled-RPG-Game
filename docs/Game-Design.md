# Game Design

## Confirmed requirements

- An RPG video game.
- A fantasy setting.
- Turn-based gameplay and combat.
- The player starts with one character and can build a party by recruiting characters they meet in the game.
- The player can create their own starting character or choose a generated character.
- The game is backed by an LLM that generates characters.
- The LLM generates every NPC the player meets, including potential recruitable companions.
- The LLM controls NPC dialogue and reactions.
- Every character has a character sheet with stats. NPC dialogue and reactions must reflect the responding character's stats and current condition; for example, a fatigued character may give disoriented responses.
- Design planning is a collaboration with the user.

## Open decisions

Resolve these through discussion, recording each agreed decision below.

1. Character creation: customization choices, generated-character selection, recruitment conditions, and party size.
2. Target platform and controls.
3. Presentation: 2D or 3D, camera perspective, and visual style.
4. Combat: battle layout, movement, initiative, actions, resources, and victory conditions.
5. World: tone, magic, cultures, central conflict, and exploration structure.
6. Characters: party size, recruitment, classes, progression, and equipment.
7. Story: player role, choices, quest structure, and intended scope.
8. Production: engine, available time, budget, asset sources, and licensing.
9. Accessibility, difficulty options, save behavior, and tutorial approach.
10. LLM generation: which character details it generates, generation timing, persistence, and local or hosted execution.

## Character creation and LLM generation

Confirmed: the player can create their own character or choose a generated character. An LLM provides character generation and generates every NPC the player meets, including potential recruitable companions.

Proposal for discussion: use the LLM to generate names, personalities, backgrounds, motivations, and character concepts. Let explicit game rules validate classes, attributes, abilities, and starting equipment so generated characters follow the same balance rules as custom characters.

Still open: whether the LLM also selects mechanical details within those rules or is limited to narrative details; whether generated starting characters are editable before selection; and whether players converse through free text, dialogue choices, or both.

## Character sheets, dialogue, and reactions

Confirmed: every character has a character sheet with stats. The LLM controls NPC dialogue and reactions and must respond in accordance with those stats and the character's current condition. A fatigued character may give disoriented responses.

Proposal for discussion: distinguish enduring attributes and personality from changing conditions such as fatigue, injury, fear, or intoxication. Provide the responding NPC's current sheet, relevant memories, and immediate situation to the LLM for each interaction. Keep game state authoritative so generated dialogue reflects current values rather than inventing changes to them.

Still open: the character sheet fields, condition severity and recovery rules, how conditions affect combat as well as dialogue, and whether personality or relationships influence recruitment and cooperation.

## Proposed first playable slice

This is a starting proposal, pending design decisions:

- One small location and a short quest.
- Demonstrate both custom character creation and selection of an LLM-generated character.
- Enough playable characters to demonstrate the chosen combat style.
- Meet one recruitable companion and demonstrate a battle with that companion.
- Demonstrate NPC dialogue and reactions that change with the NPC's character-sheet state, including fatigue.
- A small set of enemies, abilities, and equipment.
- One complete battle loop: enter combat, take turns, win or lose, and return to exploration.
- A reward and basic character progression.
- Save and load the player's progress.

Use this slice to establish whether combat and exploration are enjoyable before expanding the world.

## Decision log

| Date | Decision | Status |
| --- | --- | --- |
| 2026-10-08 | Fantasy RPG video game with turn-based gameplay | Confirmed by user |
| 2026-10-08 | Start with one character; build a party from characters met during the game | Confirmed by user |
| 2026-10-08 | Create a custom starting character or choose a generated character | Confirmed by user |
| 2026-10-08 | Use an LLM to generate characters | Confirmed by user |
| 2026-10-08 | The LLM generates every NPC the player meets, including potential companions | Confirmed by user |
| 2026-10-08 | The LLM controls NPC dialogue and reactions | Confirmed by user |
| 2026-10-08 | Every character has a stat sheet; LLM responses reflect stats and conditions, including fatigue | Confirmed by user |
| 2026-10-08 | Untitled RPG Game as working repository title | Temporary placeholder |

## Planning sequence

Agree on the player experience, define combat and exploration, outline the world and characters, then select technology and turn the first playable slice into scoped issues with acceptance criteria.
