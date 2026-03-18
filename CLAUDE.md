# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

VibeinFine is a collection of browser-based games and a small FastAPI backend, all kept in a single flat directory. The primary project is a retro top-down shooter game (`shooter.html`).

## Architecture

### Browser Games (HTML)
- **`shooter.html`** — Main project. Single-file retro top-down shooter with 10 levels, 4 enemy types, boss fights, pixel-art sprites rendered as code arrays, procedural Web Audio sound, and particle effects. All HTML/CSS/JS in one file, zero dependencies.
- **`gpuslicer.html`** — Fruit Ninja-style game where you slash NVIDIA GPUs. Features 9 GPU models with rarity tiers, combo system, bombs, particle effects, procedural Web Audio, and touch support. Single file.
- **`tictactoe.html`** — Simple tic-tac-toe game, single file.

Games are opened directly in a browser (double-click or `start shooter.html`). No build step, no bundler, no server needed.

### FastAPI Backend
- **`main.py`** — Minimal FastAPI app with `/` and `/health` endpoints.
- **`requirements.txt`** — Dependencies: `fastapi`, `uvicorn`.
- Run with: `pip install -r requirements.txt && uvicorn main:app --reload`

## Key Conventions

- **Single-file HTML games**: Each game is fully self-contained (HTML + CSS + JS) with no external assets or dependencies. Sprites are pixel arrays rendered via canvas `fillRect`.
- **No build tooling**: No npm, webpack, or transpilation. Edit and refresh.
- **Git workflow**: After every meaningful change, commit with a clean descriptive message and push to GitHub (`origin` = `https://github.com/Giambac/VibeinFine.git`). Never leave work uncommitted or unpushed — the remote must always reflect the latest state so we can revert if needed. Commit frequently (after each feature, fix, or logical unit of work), not just at the end of a session.

## shooter.html Code Sections (in order)

1. **Config & Constants** — `CFG` object, `PALETTE`, `LEVELS` array (10 levels)
2. **Sprite Data** — Pixel arrays for player (3 frames), 4 enemy types, `drawSprite()` renderer
3. **Core Engine** — `requestAnimationFrame` loop, game state machine (`menu|playing|levelComplete|gameOver|victory`), input handling
4. **Player** — Movement, aiming (atan2 to mouse), shooting with cooldown/reload, invincibility frames
5. **Bullets & Collision** — Circle-vs-circle collision, player and enemy bullet arrays
6. **Enemy System** — Walker/Runner/Tank/Boss with distinct AI behaviors, boss multi-phase
7. **Level System** — Wave-based spawning, level progression logic
8. **UI Screens & HUD** — Menu, HUD overlay, level complete/game over/victory screens
9. **Particles & Polish** — Particle system, screen shake
10. **Sound** — Web Audio API procedural sounds (shoot, hit, explosion, level complete)
