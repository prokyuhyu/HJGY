# Context: Duel Arena

## 1. Project Overview
Duel Arena is an online real-time 1v1 PvP duel game. Two players connect to the same
room and fight in a top-down arena, shooting projectiles at each other while dodging
incoming fire. This project is separate and independent from the existing "Jump Dash"
platformer project — its own repo, its own `context.md`/`CLAUDE.md`, no shared code.

## 2. Tech Stack
- **Client**: Phaser 3 + Vite + vanilla JavaScript (ES Modules) + `socket.io-client`
- **Server**: Node.js + Express + Socket.io
- **Visual style**: Shapes and colors only, no image/sprite assets for v1

## 3. Folder/File Structure
```
project-root/
├── context.md
├── CLAUDE.md
├── client/
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── src/
│       ├── main.js
│       ├── scenes/
│       │   ├── LobbyScene.js
│       │   ├── GameScene.js
│       │   └── ResultScene.js
│       ├── entities/
│       │   ├── Player.js
│       │   └── Projectile.js
│       ├── network/
│       │   └── socketClient.js
│       └── config/
│           └── gameConfig.js
└── server/
    ├── package.json
    ├── index.js
    ├── rooms/
    │   └── RoomManager.js
    └── game/
        └── DuelState.js
```

## 4. Core Game Mechanics
- **Camera/view**: Top-down arena view.
- **Combat style**: Players shoot projectiles at each other and dodge. No melee, no
  push/territory mechanics.
- **Health model**: Each player has 5 HP. Each hit = -1 HP. HP reaching 0 = defeat;
  the round ends and the game transitions to `ResultScene`, which offers a rematch
  option.
- **Networking model**: Server-authoritative. The server (Node.js + Socket.io) holds
  the true game state (position, HP, projectiles) per room and broadcasts it to both
  clients on a fixed tick. Clients send input only — never position or hit outcomes.
- **Matchmaking**: No accounts, no database. A player creates a room and receives a
  short room code; the other player joins by entering that code. The room lives in
  server memory only and closes on disconnect.

## 5. Decision Log
- 2026-08-13: Duel Arena is a separate, independent project from Jump Dash (own repo,
  own context.md/CLAUDE.md, no shared code) — keeps the two games from entangling
  their codebases or docs.
- 2026-08-13: Combat is projectile shoot-and-dodge, not melee or push/territory — sets
  the core interaction loop for the duel.
- 2026-08-13: Camera is top-down arena view — fits a symmetric 1v1 duel space better
  than side-view.
- 2026-08-13: Each player has 5 HP, -1 per hit, 0 HP ends the round into ResultScene
  with a rematch option — simple, readable win condition for a fast-paced duel.
- 2026-08-13: Networking is server-authoritative via Node.js + Socket.io, with the
  server owning position/HP/projectiles per room on a fixed tick and clients sending
  input only — prevents client-side cheating on hits and position.
- 2026-08-13: Matchmaking uses no accounts/database — room creation yields a short
  code, the other player joins with it, room state lives only in server memory and
  closes on disconnect — keeps v1 infrastructure minimal.
- 2026-08-13: Visual style is shapes/colors only, no image/sprite assets for v1 —
  consistent with the Jump Dash project's convention, keeps v1 scope small.
- 2026-08-13: Tech stack is client = Phaser 3 + Vite + vanilla JS (ES Modules) +
  socket.io-client, server = Node.js + Express + Socket.io — reuses the team's known
  Phaser/Vite workflow and pairs it with the standard Socket.io realtime stack.
- 2026-08-13: Folder structure is finalized as `client/` (Phaser+Vite app) and
  `server/` (Node/Express/Socket.io app) under this project root, per the tree in
  Section 3 — clean separation between client and server code/deploys. Note: this
  project folder was previously used for the "Jump Dash" platformer's docs-only
  draft, which is now shelved in favor of Duel Arena; Jump Dash's prior docs remain
  recoverable via git history ("First commit") if ever needed.
- 2026-08-13: Upgraded core dependencies to their latest major versions ahead of any
  gameplay/networking implementation: client = Phaser 4.2.1, Vite 8.2.1,
  socket.io-client 4.8.3; server = Express 5.2.1, socket.io 4.8.3. Done now, while
  all client/server files are still empty stubs, so there's no gameplay or
  networking code to migrate — upgrading later, after that logic exists, would mean
  a costlier migration across a larger, working codebase.

## 6. Current Status
- [x] Decisions settled: scope, combat style, camera, health model, networking model,
      matchmaking, visual style, tech stack
- [x] Folder/file structure defined
- [x] Project scaffolding (Vite client + Node/Express/Socket.io server) — structure
      and stub files only, no gameplay/networking logic yet
- [ ] Room creation/join flow
- [ ] Server-authoritative game loop (movement, projectiles, hit detection)
- [ ] Client rendering (arena, players, projectiles, HP UI)
- [ ] ResultScene + rematch flow

> This document will keep being updated as work progresses. New decisions are
> appended to the Decision Log with a new dated entry, never by silently rewriting
> earlier sections. If structure or mechanics change, update this document first,
> then note the change in the prompt sent to Claude Code.
