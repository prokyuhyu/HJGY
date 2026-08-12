# CLAUDE.md — Project Rules

This document defines the rules Claude Code must follow on this project.

## Core Principles
1. **Ask when unsure.** If structure, mechanics, or library choices are ambiguous, do not decide unilaterally — ask before proceeding.
2. **Break work into small steps.** Do not implement a large feature all at once. Implement a small unit → confirm → move to the next step.
3. **The user has final say.** When there are multiple options, present them and wait for the user's choice.
4. **Work from `context.md`.** Follow `context.md` for folder structure, file paths, and game mechanics. If the structure needs to change during implementation, notify the user first, update `context.md`, and then proceed.

## Code Rules
- Confirm with the user before adding any new npm package.
- Confirm before adding external assets (images/audio) — currently shape/color-based visuals only, no image assets.
- Keep commits small and readable, organized by file/feature.
- After implementing, briefly summarize what was done and what's next.

## Communication Rules
- **Language**: Chat responses to the user are in Korean. Project documentation (`context.md`, `CLAUDE.md`) and prompts sent to Claude Code are written in English, to save tokens.
- If a spec is unclear or you get stuck, ask before writing code.
- Big changes (folder structure, swapping libraries, etc.) require prior confirmation.

## Current Confirmed Stack
- Phaser 3 + Vite + Vanilla JS (ES Modules)
- Visuals: Shape/color-based, no image assets

> When this file itself is edited, note in the prompt/commit message what rule changed and why.
