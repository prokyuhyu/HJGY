# Context: [Game Name TBD - working title "Jump Dash"]

## 1. Project Overview
- **Genre**: Arcade platformer
- **Core gameplay**: Player jumps to avoid obstacles/enemies and survives as long as possible. Colliding ends the game; the longer you survive, the higher the score.
- **Platform**: Web browser (mobile support TBD)
- **Visual style**: No sprite images — represented with shapes (rectangles/circles) and colors. Structure is kept separate so image assets can be swapped in later if needed.

## 2. Tech Stack
- **Game engine**: Phaser 3 (Arcade Physics)
- **Bundler/dev server**: Vite
- **Language**: JavaScript (ES Modules)
- **Deployment**: Static build via `vite build` → hosting method TBD

## 3. Folder/File Structure
```
project-root/
├── index.html
├── package.json
├── vite.config.js
├── context.md            # this file
├── CLAUDE.md             # project rules
├── src/
│   ├── main.js             # Phaser game init, config
│   ├── scenes/
│   │   ├── MenuScene.js      # start screen
│   │   ├── GameScene.js      # actual gameplay
│   │   └── GameOverScene.js  # results screen
│   ├── entities/
│   │   ├── Player.js         # player (shape-based)
│   │   └── Obstacle.js       # obstacles/enemies
│   └── config/
│       └── gameConfig.js     # resolution, physics constants, etc.
└── public/                # static assets (e.g. sound, if added later)
```

## 4. Core Game Mechanics (Draft — pending discussion)
- **Controls**: Spacebar or click/tap = jump
- **Movement**: Player fixed on the left side of the screen; background/obstacles scroll right-to-left (temporary — ⚠️ needs discussion, could switch to free left/right movement)
- **Collision**: Touching an obstacle ends the game immediately → transitions to GameOverScene
- **Score**: Based on survival time or distance traveled (⚠️ needs to be finalized)
- **Difficulty**: Obstacle speed/frequency increases over time (to be tuned later)

## 5. Current Status (progress checklist)
- [ ] Initial setup (create Vite + Phaser project)
- [ ] Implement MenuScene
- [ ] GameScene skeleton (player movement/jump)
- [ ] Obstacle spawn logic
- [ ] Collision/game-over handling
- [ ] Score UI
- [ ] Polish (sound, effects, etc. — lower priority)

> This document will keep being updated as work progresses. If structure or mechanics change, update this document first, then note the change in the prompt sent to Claude Code.
