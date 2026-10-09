# Untitled RPG Game

A fantasy video game with turn-based combat, currently in collaborative design planning.

The player starts alone and can build a party from characters they meet in the game. The name is a placeholder. Platform, engine, visual style, party size, setting, and story are still to be decided. Combat will use a 3D battlefield with a rotatable camera.

The MVP consists of the combat, character, party, and dungeon systems and will be playable without an LLM. Characters move around a tactical grid, and the display accounts for terrain height and flying characters. Combat outcomes are resolved by the combat system, with status effects able to affect actions.

The full game will let players create their own starting character or choose a generated character. Post-MVP, an LLM will generate characters, including every NPC the player meets, and control NPC dialogue and reactions according to each character's stat sheet and condition. The LLM may submit combat commands, but the combat system determines their outcomes.

## Planning

- [Game design](docs/Game-Design.md): confirmed requirements, open decisions, and a proposed first playable slice.
- [Repository workflow](docs/Repository-Workflow.md): branches, issue flow, and validation requirements.
- [Planning board](https://github.com/users/darkdhamon/projects/11): work tracked from Backlog through Released.

There is no playable build yet.

## Development

`dev` is the base for ongoing development. `main` is reserved for releases after initial repository setup. Application changes start with a GitHub issue and use a feature branch and pull request.

No software or asset license has been selected yet.
