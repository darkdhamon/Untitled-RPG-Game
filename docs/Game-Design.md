# Game Design

## Confirmed requirements

- An RPG video game.
- A fantasy setting.
- Turn-based gameplay and combat.
- The combat system owns combat rules and outcomes. The LLM may submit commands to it but does not determine outcomes.
- Status effects may affect actions in the combat system.
- Each character gets one attack of opportunity per ready weapon, usable outside their turn per round. These allowances reset on that character's turn.
- Characters can move around a tactical grid. The display must account for terrain height and flying characters.
- Combat uses a 3D battlefield with a rotatable camera.
- The tactical grid is square.
- Diagonal movement is allowed. Characters cannot move through blocked squares.
- Blocked orthogonal neighbors do not prevent a diagonal step: if N and W are blocked, a character may still move NW when the NW square is traversable.
- Movement range sums the Euclidean length of every step along the traversed route, including diagonal steps, then rounds the total to the nearest whole number. That rounded total must not exceed the character's effective movement for the turn, and the route must respect blocked squares.
- MVP systems: combat, characters, parties, and dungeons. LLM features are outside the MVP.
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
3. Presentation: visual style, presentation outside combat, and camera controls for the 3D battlefield.
4. Combat: square-grid movement rules, elevation and flight rules, initiative, actions, resources, and victory conditions.
5. World: tone, magic, cultures, central conflict, and exploration structure.
6. Characters: party size, recruitment, classes, progression, and equipment.
7. Story: player role, choices, quest structure, and intended scope.
8. Production: engine, available time, budget, asset sources, and licensing.
9. Accessibility, difficulty options, save behavior, and tutorial approach.
10. LLM generation: which character details it generates, generation timing, persistence, and local or hosted execution.
11. Dungeons: layout, exploration, encounters, completion rules, and authored or procedural content.

## MVP scope

Confirmed MVP systems:

| System | Confirmed scope | Details to decide |
| --- | --- | --- |
| Combat | Turn-based combat with square-grid movement on a 3D battlefield and a rotatable camera; display accounts for terrain height and flying characters; combat system resolves outcomes; status effects may affect actions | Movement rules, elevation and flight rules, camera controls, turn order, available actions, resolution rules, and status effects |
| Characters | Characters with stat sheets | Attributes, creation options for MVP, abilities, equipment, and progression |
| Parties | Start with one character and build a party from characters encountered | Recruitment rules, party size, and control of party members |
| Dungeons | A dungeon system | Layout, exploration, encounters, completion rules, and content creation |

All LLM features are post-MVP: LLM character generation, NPC dialogue and reactions, and any LLM submission of combat commands. The MVP must be playable without an LLM.

Proposal for discussion: use predefined NPCs and simple rules-based enemy behavior for the MVP, then integrate LLM features into the existing systems later. The non-LLM method for offering generated starting characters remains undecided.

## Combat authority

Confirmed: the underlying combat system is not controlled by the LLM. The LLM may send commands, but the combat system determines their outcomes. Status effects may affect combat actions.

Proposal for discussion: all action sources use the same command interface. The combat system validates the acting character, turn, targets, costs, and status restrictions, resolves the action using game rules, and records the resulting state. A future LLM can request an action and receive its result without directly changing health, status effects, or other combat state.

## Attacks of opportunity

Confirmed: each character has one attack of opportunity per ready weapon to use outside their turn per round. The allowances reset on that character's turn. The allowance is per weapon rather than one shared attack of opportunity for the entire character.

Confirmed example: a character holding one ready dagger in each hand can choose to attack with one dagger or both in response to a provoking event. If both are used, the second attack is at disadvantage. Each weapon used consumes its own attack-of-opportunity allowance; an unused weapon retains its allowance.

Still open:

- Which events provoke an attack of opportunity, including movement within or out of an opponent's reach.
- What counts as a ready weapon and how weapon changes affect its allowance.
- Whether the two-dagger rule applies to other combinations of ready weapons.
- Unanswered question: should disadvantage mean rolling twice and using the lower result? The user has not decided whether to model the rules after D&D or GURPS. No dice mechanic or rules direction is selected. The second dual-dagger attack remains subject to disadvantage, with its mechanical definition pending.
- How disadvantage interacts with other modifiers.
- The precise reset timing within the character's turn.
- Whether movement can be split around actions. The user tentatively supported this while raising attacks of opportunity; it is not yet a confirmed rule.

A Disengage action has been suggested but is not a confirmed requirement.

## Tactical grid, elevation, and flight

Confirmed: characters can move around a square grid on a 3D battlefield with a rotatable camera. The display must account for terrain height and flying characters. These are requirements for the MVP combat system.

Proposal for discussion: track terrain elevation separately from a character's height above the terrain, so a grounded character on a raised platform and a flying character above that platform can be represented distinctly. Make the occupied grid position and height readable through visual indicators. Camera tilt, zoom, panning, rotation behavior, and the rendering style remain undecided.

Still open:

- How multiple moves consume the turn's movement allowance and exact halfway rounding behavior.
- Discrete height levels or continuous height values.
- Whether flight allows different characters to occupy the same horizontal cell at different heights.
- Climbing, jumping, falling, takeoff, landing, and flight restrictions.
- How elevation and flight affect movement costs, attack range, line of sight, cover, and targeting.
- Camera controls and how the display handles characters obscured by terrain or other characters.

### Movement range

Confirmed: diagonal movement is allowed, and characters cannot move through blocked squares. Measure the Euclidean length of each step along the actual route, sum those lengths, and round the total to the nearest whole number. A move is within range when that rounded route length does not exceed the character's effective movement for the turn. Do not use straight-line displacement between the start and destination or round individual steps.

For a flat grid with one distance unit per square, each N/S/E/W step has length `1`, and each diagonal step has length `sqrt(2)` (approximately `1.414`). The move's cost is `roundNearest(sum(stepLengths))`.

User example: a destination two squares north and one square west can be reached by stepping NW, then N. The route length is `sqrt(2) + 1`, approximately `2.414`, which rounds to a movement cost of `2`. A route N, N, W to the same destination has length `3` and costs `3`. Detours therefore count toward movement range.

Still open: elevation and flight distance rules, exact halfway rounding behavior, and how movement costs accumulate when a character makes multiple separate moves during one turn.

Movement validation must check both the distance allowance and a traversable route. Passing the distance check does not authorize crossing blocked squares.

Diagonal steps may pass between blocked orthogonal neighbors. For example, blocked N and W squares do not prevent a step into a traversable NW square. Route validation must not reject that diagonal step solely because its adjacent orthogonal squares are blocked; the character still cannot enter a blocked destination square.

## Character creation and LLM generation

The LLM features in this section are post-MVP requirements.

Confirmed: the player can create their own character or choose a generated character. An LLM provides character generation and generates every NPC the player meets, including potential recruitable companions.

Proposal for discussion: use the LLM to generate names, personalities, backgrounds, motivations, and character concepts. Let explicit game rules validate classes, attributes, abilities, and starting equipment so generated characters follow the same balance rules as custom characters.

Still open: whether the LLM also selects mechanical details within those rules or is limited to narrative details; whether generated starting characters are editable before selection; and whether players converse through free text, dialogue choices, or both.

## Character sheets, dialogue, and reactions

Character sheets are MVP. LLM dialogue and reactions are post-MVP.

Confirmed: every character has a character sheet with stats. The LLM controls NPC dialogue and reactions and must respond in accordance with those stats and the character's current condition. A fatigued character may give disoriented responses.

Proposal for discussion: distinguish enduring attributes and personality from changing conditions such as fatigue, injury, fear, or intoxication. Provide the responding NPC's current sheet, relevant memories, and immediate situation to the LLM for each interaction. Keep game state authoritative so generated dialogue reflects current values rather than inventing changes to them.

Still open: the character sheet fields, condition severity and recovery rules, the specific effects of conditions on combat actions and dialogue, and whether personality or relationships influence recruitment and cooperation.

## Proposed first playable slice

This is a proposal for an MVP slice covering the four confirmed systems, pending detailed design decisions:

- One small dungeon with an entrance, encounters, and a completion objective.
- A 3D grid encounter with a rotatable camera, raised terrain, and a flying character to demonstrate readable positions and heights.
- A starting character with a stat sheet and the agreed MVP creation options.
- One predefined recruitable companion and a battle with that companion.
- A small set of enemies, abilities, and equipment.
- One complete battle loop: enter combat, take turns, resolve outcomes through the combat system, win or lose, and return to dungeon exploration.
- At least one status effect demonstrating its impact on combat actions.
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
| 2026-10-08 | Combat system resolves outcomes; the LLM may submit commands but does not determine outcomes | Confirmed by user |
| 2026-10-08 | Status effects may affect combat actions | Confirmed by user |
| 2026-10-08 | One out-of-turn attack of opportunity per ready weapon per round; allowances reset on the character's turn | Confirmed by user |
| 2026-10-08 | A character with a dagger in each hand may use one or both for an attack of opportunity; the second attack is at disadvantage when both are used | Confirmed by user |
| 2026-10-08 | Definition of disadvantage; whether to model rules after D&D or GURPS | Unanswered; deferred by user |
| 2026-10-08 | Combat, character, party, and dungeon systems are MVP; LLM features are post-MVP | Confirmed by user |
| 2026-10-08 | Characters move around a grid; display accounts for terrain height and flying characters | Confirmed by user |
| 2026-10-08 | A 3D battlefield with a rotatable camera | Confirmed by user |
| 2026-10-08 | Use a square tactical grid | Confirmed by user |
| 2026-10-08 | Allow diagonal movement; prohibit movement through blocked squares | Confirmed by user |
| 2026-10-08 | Allow diagonal passage between blocked orthogonal neighbors; blocked N and W do not prevent movement into traversable NW | Confirmed by user |
| 2026-10-08 | Sum Euclidean lengths of route steps, then round the total to nearest; cost must not exceed effective movement for the turn | Confirmed by user; clarified with NW then N costing 2 |
| 2026-10-08 | Untitled RPG Game as working repository title | Temporary placeholder |

## Planning sequence

Define the MVP combat, character, party, and dungeon systems, choose a platform and technology, then turn the first playable slice into scoped issues with acceptance criteria. Preserve LLM requirements for post-MVP integration.
