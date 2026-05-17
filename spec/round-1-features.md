<!--
---
title: "Round 1 Features"
description: "Curated feature list for the first development round"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: specification
  - domain: [game, specs]
  - tech: [javascript, html, css, canvas]
---
-->

# Round 1 Features

The first participant builds the baseline (see `baseline.md`), then picks **3 to 5 features** from this list. These are the first additions to the game. They're selected to be visually rewarding and self-contained: each one makes the game noticeably better without requiring changes to the others.

For each feature you pick, write a short spec with your AI assistant describing what you want. The spec should say what it looks like when it's working and what "wrong" looks like. The AI builds it. Playtest. Iterate until satisfied. Commit everything on your branch and open a PR for review.

---

## The Menu

### Particle Effects

When a brick breaks, it bursts into small colored particles that scatter outward and fade. The particles match the brick's color. The effect is brief (under half a second) and does not interfere with gameplay. Particles do not interact with the ball or paddle.

**What good looks like:** Breaking a brick feels satisfying. The particles add energy without cluttering the screen. The effect works with the pixel art style (small square particles rather than smooth circles keep the aesthetic consistent).

**Watch for:** Particles that persist too long, slow down the game, or obscure the ball.

---

### Ball Trail

The ball leaves a fading trail behind it as it moves. The trail is a series of progressively smaller and more transparent copies of the ball sprite (or simple circles) along the ball's recent path. The trail makes the ball easier to track at speed.

**What good looks like:** The ball looks like a comet. The trail fades smoothly over about 5 to 10 frames. The pixel art style is maintained.

**Watch for:** Trail that never fades, trail that causes visual flickering, trail that makes the ball's current position ambiguous.

---

### Sound Effects

Distinct sounds for: paddle hit, brick break, wall bounce, life lost, game win, and game over. Use the Web Audio API to generate simple synthesized tones or noise bursts (no audio files needed for SFX). Each sound should be short and distinct enough that a player can tell what happened by sound alone.

The `assets/cosmic-breakout-html-game-template-free/` directory contains a complete breakout game that uses procedural Web Audio for all its sound effects. Study it as a reference for what synthesized game audio sounds like and how different events get distinct sonic signatures.

**What good looks like:** The game has audio feedback for every meaningful event. Sounds are pleasant, not grating. Volume is consistent. Sounds fit the retro pixel art aesthetic.

**Watch for:** Sounds that are too loud, too similar, or delayed. Audio glitches when multiple events happen simultaneously (e.g., ball hits two bricks on the same frame). Sounds that play during pause.

---

### Background Music

A looping music track plays during gameplay. Music loops are included in `assets/music/` (Torone loop pack, .ogg format). The gameplay tracks (`sf-action-1.ogg`, `sf-action-2.ogg`) work well for in-game music. The title/menu track (`sf-title-menu-credit.ogg`) can play on the start screen if one exists.

Music should have a volume control or at minimum a mute toggle. Music pauses when the game is paused and resumes when unpaused. Music volume should sit below sound effects so SFX remain audible.

**What good looks like:** The music creates atmosphere without dominating. It loops seamlessly. Pausing the game pauses the music. The player can mute it.

**Watch for:** Music that restarts from the beginning on each loop (should be seamless). Music that keeps playing when the game is paused. Music drowning out sound effects. Browser autoplay policies blocking audio (the first user interaction should unlock audio context).

---

### Speed Ramp

The ball gets slightly faster each time a brick is broken. The increase is subtle enough that the player doesn't notice it per-brick but feels it over the course of a level. By the time only a few bricks remain, the game is noticeably harder than when it started.

**What good looks like:** Early game feels relaxed. Late game feels tense. The transition is smooth, not stepped.

**Watch for:** Ball becoming impossibly fast before the level is half cleared. Speed not resetting between lives (decide whether it should). Ball moving so fast it passes through bricks without registering a hit (collision detection needs to handle high speeds).

---

### Level Progression

After clearing all bricks, a new level loads with a fresh brick layout. At least 3 levels. Each level can have a different brick arrangement (centered block, checkerboard, pyramid, frame shape, diagonal stripes). The score carries between levels. Lives carry between levels.

Level layouts should use different block sprites or color arrangements from the asset pack to make each level visually distinct.

**What good looks like:** Clearing a level feels like an accomplishment. The new layout is visibly different. A brief "Level 2" message appears before play resumes. The ball resets to the paddle between levels.

**Watch for:** Score or lives resetting between levels. Ball launching automatically without player input. Brick layouts that leave unreachable bricks.

---

### Score Display Polish

The score and lives display is styled and positioned intentionally. Score in the top-left or top-center, lives in the top-right (as a number or as small sprite icons). A current level indicator if level progression is included.

Use one of the pixel fonts from `assets/fonts/` (the OPF or Pixbob families) loaded via `@font-face`. The font should match the pixel art aesthetic of the sprites.

**What good looks like:** The HUD feels like part of the game, not an afterthought. Information is findable without looking for it. The pixel font ties the UI to the game's visual style.

**Watch for:** Text that overlaps the play area. Font too small on larger screens. Font failing to load (have a fallback). Lives display not updating.

---

## After You Pick

Pick 3 to 5 features from this menu.

1. Write a spec for each feature with your AI assistant
2. Build the baseline first, playtest it, make sure it's solid
3. Add features one at a time
4. Playtest after each feature
5. Commit after each working feature
6. When satisfied, push your branch and open a PR for your teammate to review
7. Your reviewer will playtest the game and either approve or leave feedback
