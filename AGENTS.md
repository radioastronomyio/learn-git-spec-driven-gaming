<!--
---
title: "Agent Instructions"
description: "Repository context, constraints, and conventions for AI assistants"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: guide
  - domain: [documentation, specs]
related_documents:
  - "[Repository Root](README.md)"
  - "[Baseline Spec](spec/baseline.md)"
  - "[AI Interaction Instructions](docs/ai-instructions.md)"
  - "[Documentation Standards](docs/documentation-standards/README.md)"
---
-->

# Agent Instructions

## Repository Identity

This is a Git and spec-driven development training repository. Participants learn Git workflow by building a browser-based Breakout game through rounds of spec, build, review, and merge. The game is built entirely by AI assistants from specs; participants validate through playtesting, not code review.

Repository: `learn-git-spec-driven-gaming`

## Context Loading

Load context in this order:

1. This file (`AGENTS.md`) for repository identity, constraints, and conventions
2. `docs/ai-instructions.md` for behavioral guidelines on interacting with participants
3. `README.md` for project overview, round structure, and current state
4. `spec/baseline.md` for the minimum viable Breakout definition
5. The specific spec or feature menu for the current round
6. `docs/documentation-standards/` for templates and standards to follow

## Architectural Constraints

- The game is an HTML file (`game/index.html`) with embedded CSS and JavaScript, loading sprite images and other assets from `game/assets/`.
- No frameworks, no build tools, no CDN imports, no server required. The game must work by opening `game/index.html` directly in a browser.
- Canvas API for rendering. No DOM-based game elements.
- All game features must be playable in a standard browser without installation.
- Participants never write code directly. All code changes come through AI execution of specs.

## Asset Pack

The repository includes a pixel art asset pack and supporting resources in `assets/`. These are the source files. When building the game, copy the needed assets into `game/assets/` where the game code references them.

### Sprites (Pixeltier Breakout Asset Pack)

Located in `assets/pixeltiers-breakout-asset-pack/`. Free for personal and commercial use. No redistribution of the pack itself.

**Paddles:** 4 styles × 3 sizes (small, mid, large) × 5 metallic colors (beige, brown, gold, grey, silver). Located in `paddles/`. Naming pattern: `paddle_{style}_{size}_{color}.png`. The size variants support the grow power-up visually.

**Blocks:** 5 intact types + 3 damage states, in standard and mid sizes, across 12 colors (black, blue, brown, gold, green, lightblue, orange, pink, purple, red, silver, yellow). Located in `blocks/`. Naming patterns:
- Intact: `block_{type}_{color}.png` and `block_{type}_mid_{color}.png`
- Damaged: `block_broken_{level}_{color}.png` and `block_broken_{level}_mid_{color}.png` where level is 1, 2, or 3
- Gloss overlay: `blocks/gloss_animation/gloss_animation_{1-3}.png` (3-frame shimmer)

**Balls:** 4 designs, some with animation frames, in 12 colors. Located in `balls/`. Naming pattern: `ball_{design}_{color}.png` or `ball_{design}_{color}_{frame}.png`.

**Power-ups:** 7 types with 4-frame animations. Located in `powerups/`. Types: extraball, grow, powerball, reverse, shield, split, twinballs. Naming pattern: `powerup_{type}_{frame}.png`.

**Background:** Star sky in two resolutions. `background.png` and `background-400.png`.

**Spritesheet:** `spritesheet_assets.png` contains all sprites on one sheet. Individual files are also provided.

### Fonts

Located in `assets/fonts/`. Two pixel font families:
- OPF (Owlish Pixel Fonts): `opf-large.ttf`, `opf-medium.ttf`, `opf-small.ttf`
- Pixbob: `pixbob-lite.ttf`, `pixbob-tall lite.ttf` (and .otf variants)

### Music

Located in `assets/music/`. Torone loop pack in .ogg format:
- Gameplay: `231006-torone-loop-pack-02-sf-action-1.ogg`, `sf-action-2.ogg`
- Title/menu: `231006-torone-loop-pack-02-sf-title-menu-credit.ogg`
- Stingers: `sf-explo-1.ogg`, `sf-explo-2.ogg`, `sf-explo-3.ogg`

### Reference Material

`assets/cosmic-breakout-html-game-template-free/` contains a complete single-file breakout game (MIT licensed). It uses procedural Web Audio for all sound effects (17 synthesized SFX, zero audio files). Study it as reference for sound synthesis patterns, game feel, and feature implementation. Do not copy its code directly; use it to understand approaches.

## Pixel Art Rendering

All sprites are pixel art. Render them at integer scale (2x, 3x, 4x depending on canvas size) using nearest-neighbor interpolation. In Canvas 2D, set `context.imageSmoothingEnabled = false` before drawing sprites. Avoid sub-pixel positioning that would blur the art.

## Game Directory Structure

```
game/
├── index.html          # All game CSS and JavaScript
└── assets/
    ├── sprites/        # Paddle, ball, block, power-up PNGs
    ├── fonts/          # Pixel font files
    ├── audio/          # Music loops (if music feature is implemented)
    └── background.png  # Star sky background
```

Only copy assets from `assets/` into `game/assets/` as features require them. The baseline needs one paddle sprite, one ball sprite, 5+ block color variants, and the background. Additional sprites (power-ups, damage states, alternate paddles) are added in later rounds.

## Sound Design

Sound effects use the Web Audio API to generate synthesized tones and noise bursts at runtime. No audio files for SFX. This keeps the game dependency-light and makes sounds programmatically adjustable.

Background music (if implemented) uses the .ogg files from the music directory. Music and SFX are independent systems with separate volume controls.

## Documentation Conventions

- All Markdown files require YAML frontmatter (see `docs/documentation-standards/tagging-strategy.md`)
  - Exempt: README files that serve as simple pointers (e.g., `CLAUDE.md`) and source materials in `internal-files/`
- New directories require an interior README (see `docs/documentation-standards/interior-readme-template.md`)
- Follow writing style conventions (see `docs/documentation-standards/writing-style-guide.md`)
- Never delete files; move unnecessary files to `recycle/` with documented justification

## Commit Messages

- Present tense, imperative mood
- 72-character first line limit
- Examples: `add particle effects on brick break`, `fix ball clipping through paddle edge`, `copy power-up sprites into game assets`

## Session Pattern

1. Load context (this file + `docs/ai-instructions.md`)
2. Read the relevant spec for the current task
3. Work within the spec's defined scope
4. Playtest by opening `game/index.html` in the browser
5. Iterate until the participant is satisfied
6. Document changes appropriately
7. Update work-logs if significant work completed
