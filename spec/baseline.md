<!--
---
title: "Baseline Spec: Minimum Viable Breakout"
description: "What the game must do before any features are added"
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

# Baseline Spec: Minimum Viable Breakout

This defines what Breakout is. Every item here is non-negotiable. The AI builds all of this before any Round 1 features are added. The first participant reviews the baseline by playing it. If any of these behaviors are missing or broken, the baseline is not complete.

---

## 1. The Game

An HTML file (`game/index.html`) containing all CSS and JavaScript, with sprite images and a background loaded from `game/assets/`. No frameworks, no CDN imports, no build tools, no server required. Open `index.html` in any modern browser and play immediately.

The `game/` directory structure:

```
game/
├── index.html
└── assets/
    ├── sprites/      # Paddle, ball, block, and power-up sprites
    ├── fonts/         # Pixel fonts
    └── background.png # Star sky background
```

Assets are copied from the repository's `assets/` directory into `game/assets/` as part of the build. The spec or AI instructions should specify which sprites to use. See `assets/pixeltiers-breakout-asset-pack/` for the full inventory.

---

## 2. Play Area

A canvas element, centered on the page. The star sky background image (`assets/pixeltiers-breakout-asset-pack/background.png`) fills the play area. The play area has solid walls on the top, left, and right sides. The bottom is open (where the ball escapes).

The canvas should be large enough to feel like a real game, not a thumbnail. Target roughly 800x600 or similar proportions that fit comfortably in a browser window without scrolling. The background image tiles or scales to fill the canvas.

---

## 3. Paddle

A paddle sprite from the asset pack, positioned at the bottom of the play area. Moves left and right with the mouse (tracks horizontal mouse position) and with left/right arrow keys or A/D keys. The paddle cannot move outside the play area walls.

Use one of the paddle sprites from `assets/pixeltiers-breakout-asset-pack/paddles/`. Pick a style and color that reads clearly against the star background. The mid-size paddle (e.g., `paddle_1_mid_silver.png`) is a good starting point.

---

## 4. Ball

A ball sprite from the asset pack that moves in a straight line, bouncing off walls, the paddle, and bricks. The ball starts resting on the paddle. The player clicks or presses Space to launch it upward at a slight angle.

Use one of the ball sprites from `assets/pixeltiers-breakout-asset-pack/balls/`. A solid, non-animated ball (e.g., `ball_1_lightblue.png`) works well for the baseline.

Bounce behavior:

- Wall bounce: angle of incidence equals angle of reflection.
- Paddle bounce: the angle changes based on where the ball hits the paddle. Center returns it mostly straight up. Edges send it at a sharper angle. This gives the player directional control.
- Brick bounce: same as wall bounce (reflect off the surface that was hit).

The ball has a constant speed in the baseline. It does not accelerate or decelerate.

---

## 5. Bricks

A grid of brick sprites near the top of the play area. At least 5 rows and 8 columns. Each row uses a different color variant of the block sprites from the asset pack. When the ball hits a brick, the brick disappears and the ball bounces.

Use block sprites from `assets/pixeltiers-breakout-asset-pack/blocks/`. The pack provides 12 color variants (black, blue, brown, gold, green, lightblue, orange, pink, purple, red, silver, yellow) across multiple block styles. Pick one block style and vary the color by row.

Example row-color mapping (top to bottom): red, orange, yellow, green, blue. Top-row bricks are harder to reach, so they're worth more points.

---

## 6. Score

A visible score counter. Each brick broken adds points. Top-row bricks are worth more than bottom-row bricks (e.g., top row = 50 pts, bottom row = 10 pts). The score is displayed on the canvas, readable at a glance.

Use one of the included pixel fonts from `assets/fonts/` for the score display, or fall back to a system monospace font if font loading adds complexity to the baseline.

---

## 7. Lives

The player starts with 3 lives. When the ball passes below the paddle (falls off the bottom), one life is lost. The remaining lives are displayed on screen (as a number or as small paddle/ball icons). After losing a life, the ball resets to the paddle and the player clicks or presses Space to relaunch.

---

## 8. Win Condition

When all bricks are cleared, the player wins. Display a "You Win" message. The game stops (the ball and paddle freeze or disappear).

---

## 9. Lose Condition

When all 3 lives are lost, the game is over. Display a "Game Over" message with the final score. The game stops.

---

## 10. Pause

Pressing Escape or P pauses the game. The ball, paddle, and any active timers freeze. A visible "Paused" indicator appears. Pressing the same key resumes play. No game input (mouse, arrow keys) is processed while paused. Only the pause key responds.

---

## 11. Restart

After winning or losing, the player can restart. A click, keypress, or visible "Play Again" prompt resets everything: bricks, score, lives, ball position.

---

## 12. Visual Minimum

The game uses pixel art sprites from the asset pack. At minimum:

- The star sky background fills the play area
- Bricks are clearly visible and distinct from the background, with different colors per row
- The ball is visible against both the background and the bricks
- The paddle is clearly distinguishable
- Score and lives are readable
- Win/lose/pause messages are readable

The sprites are pixel art. Render them at integer scale (2x, 3x, 4x) with nearest-neighbor interpolation to keep the pixels crisp. Avoid sub-pixel positioning or anti-aliased scaling that would blur the art.

---

## 13. What the Baseline Does NOT Include

These are all Round 1, Round 2, or later features. Do not build them in the baseline:

- Sound effects or music
- Particle effects or animations beyond basic movement
- Power-ups
- Multiple levels or level progression
- Multi-hit bricks (damage states)
- Speed changes
- Ball trails or visual flourishes beyond the sprites themselves
- Brick entry or break animations

---

## 14. Asset Checklist

Before the baseline is complete, confirm these assets are in place:

| Asset | Source | Destination |
|-------|--------|-------------|
| Star background | `assets/pixeltiers-breakout-asset-pack/background.png` | `game/assets/background.png` |
| Paddle sprite (1) | `assets/pixeltiers-breakout-asset-pack/paddles/` | `game/assets/sprites/` |
| Ball sprite (1) | `assets/pixeltiers-breakout-asset-pack/balls/` | `game/assets/sprites/` |
| Block sprites (5+ colors) | `assets/pixeltiers-breakout-asset-pack/blocks/` | `game/assets/sprites/` |
| Font (optional) | `assets/fonts/` | `game/assets/fonts/` |

Only copy the assets you need for the baseline. Additional sprites (power-ups, damage states, alternate paddles) are added in later rounds as features require them.

---

## 15. Validation (Playtest Checklist)

Play through the game and verify each of these:

| Check | What to look for |
|-------|------------------|
| Game loads | `game/index.html` opens in the browser without errors, sprites display correctly |
| Background | Star sky background fills the play area |
| Ball launches | Click or Space launches the ball from the paddle at an angle |
| Paddle tracks | Paddle follows mouse smoothly, stays within walls |
| Keyboard works | Left/right arrow keys and A/D keys move the paddle |
| Wall bounce | Ball bounces correctly off top, left, and right walls |
| Paddle bounce | Ball angle changes based on hit position (center vs. edge) |
| Brick collision | Bricks disappear on contact, ball bounces |
| No pass-through | Ball never clips through a brick or wall without bouncing |
| Row colors | Each row of bricks is a different color |
| Score increments | Score goes up when bricks break, top rows worth more |
| Life lost | Ball falling below the paddle costs a life |
| Lives display | Remaining lives shown and update correctly |
| Ball resets | After losing a life, ball returns to paddle |
| Win state | Clearing all bricks shows "You Win" |
| Lose state | Losing all lives shows "Game Over" with final score |
| Pause works | Escape or P pauses and resumes, game freezes completely while paused |
| Restart works | Game can be restarted after win or loss |
| Pixel art crisp | Sprites render at integer scale without blur |
