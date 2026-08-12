# CLAUDE.md — Project Rules (Duel Arena)

This document defines the rules Claude Code must follow on this project.

## Core Principles
1. **Ask when unsure.** If structure, mechanics, or library choices are ambiguous, do
   not decide unilaterally — ask before proceeding.
2. **Break work into small steps.** Do not implement a large feature all at once.
   Implement a small unit → confirm → move to the next step.
3. **The user has final say.** When there are multiple options, present them and wait
   for the user's choice.
4. **Work from `context.md`.** Follow `context.md` for folder structure, file paths,
   and game mechanics. If the structure needs to change during implementation, notify
   the user first, update `context.md`, and then proceed.
5. **Independent from Jump Dash.** This project is a separate repo with its own
   `context.md`/`CLAUDE.md`. Do not share code, assumptions, or conventions from the
   Jump Dash platformer project unless the user explicitly asks to port something
   over.

## Code Rules
- Confirm with the user before adding any new npm package.
- Confirm before adding external assets (images/audio) — currently shape/color-based
  visuals only, no image assets.
- Keep commits small and readable, organized by file/feature.
- After implementing, briefly summarize what was done and what's next.

## Networking-Specific Rules
- **Server is authoritative.** The server owns true game state (position, HP,
  projectiles) per room. Never implement client-side authority over position or hit
  outcomes.
- **Clients send input only.** Client code sends input events (movement, aim, fire)
  to the server; it must never send — and the server must never trust — a client's
  claimed position or hit result.
- **Fixed tick broadcast.** Server state updates broadcast to both clients in a room
  on a fixed tick. Do not introduce variable/uncapped broadcast rates without
  confirming with the user first.
- **No persistence.** No accounts, no database. Room state lives in server memory
  only and is discarded on disconnect/room close. Confirm with the user before
  introducing any persistent storage.
- **Room codes, not matchmaking queues.** Players pair up via a short room code
  (create/join), not automated matchmaking. Do not add queue-based or ranked
  matchmaking without confirming with the user first.
- Confirm with the user before changing the networking library (Socket.io) or the
  server-authoritative model itself — this is a foundational architectural decision.

## Communication Rules
- Chat responses to the user are in Korean.
- Project documentation (`context.md`, `CLAUDE.md`) and prompts sent to Claude Code
  are written in English only — no bilingual clauses in these files.
- If a spec is unclear or you get stuck, ask before writing code.
- Big changes (folder structure, swapping libraries, etc.) require prior confirmation.

## Current Confirmed Stack
- **Client**: Phaser 4.2.1 + Vite 8.2.1 + vanilla JavaScript (ES Modules) +
  `socket.io-client` 4.8.3
- **Server**: Node.js + Express 5.2.1 + Socket.io 4.8.3
- **Visuals**: Shape/color-based, no image assets

> When this file itself is edited, note in the prompt/commit message what rule
> changed and why.
