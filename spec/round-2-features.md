<!--
---
title: "Round 2 Features"
description: "Curated feature list for the second development round"
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

# Round 2 Features

The second participant receives the Round 1 PR, playtests the game, and merges. Then they pick **3 to 5 features** from this list. These build on the existing foundation and focus on gameplay: how the game plays, how decisions feel, and how each round changes. Several of these features interact with each other and with Round 1 additions, so playtesting for unintended side effects matters.

Same workflow as Round 1: write a spec with your AI assistant, have the AI build it, playtest, iterate, commit, and open a PR for review.

---

## The Menu

### Power-Up Drops

When certain bricks break, a small animated icon falls toward the paddle. If the paddle catches it, the power-up activates. If it falls past the paddle, nothing happens. Power-ups are temporary (timed or single-use).

The asset pack includes 7 power-up types with 4-frame animations in `assets/pixeltiers-breakout-asset-pack/powerups/`. Include at least three of these:

| Power-up | Sprites | Suggested behavior |
|----------|---------|-------------------|
| Extra Ball | `powerup_extraball_1-4.png` | Spawns a second ball immediately |
| Grow | `powerup_grow_1-4.png` | Paddle grows to the large size sprite for 15 seconds |
| Power Ball | `powerup_powerball_1-4.png` | Ball breaks through bricks without bouncing for 5 seconds |
| Reverse | `powerup_reverse_1-4.png` | Paddle controls are inverted for 10 seconds (negative power-up) |
| Shield | `powerup_shield_1-4.png` | A temporary barrier appears at the bottom, preventing one ball loss |
| Split | `powerup_split_1-4.png` | The ball splits into three, spreading in a fan |
| Twin Balls | `powerup_twinballs_1-4.png` | Spawns two extra balls at the paddle |

Power-ups should drop from roughly 1 in 5 bricks (randomized, not predetermined). The falling icon should animate through its 4 frames while descending. A small indicator shows which power-up is active and how much time remains.

When the grow power-up activates, swap the paddle sprite to the large variant (e.g., `paddle_1_large_silver.png`). When it expires, swap back to the mid variant. This gives the power-up visual feedback through the existing art.

**What good looks like:** Power-ups add excitement and tactical decisions. Do I go for the falling power-up and risk missing the ball? The animated icons are eye-catching but not distracting. The indicator is clear without dominating the HUD.

**Watch for:** Power-ups dropping too frequently (feels spammy) or too rarely (feels pointless). Grow making the game trivially easy. Power-up icon too small to see while tracking the ball. Multiple active balls getting confusing without clear visual distinction. Timer not resetting when a new power-up replaces an active one. Power-up timers ticking during pause.

---

### Multi-Hit Bricks

Some bricks require multiple hits to break. The asset pack includes damage state sprites for each block color:

- `block_1_red.png` (intact)
- `block_broken_1_red.png` (first hit)
- `block_broken_2_red.png` (second hit)
- `block_broken_3_red.png` (third hit, then breaks)

A two-hit brick starts intact, then swaps to the `broken_1` sprite after the first hit, then breaks on the second. A three-hit brick shows three visual states before breaking. Multi-hit bricks are worth more points than single-hit bricks.

Place multi-hit bricks in the upper rows where they're harder to reach. Lower rows stay single-hit.

**What good looks like:** Multi-hit bricks are visually distinct from single-hit bricks through the damage state sprites. The damage progression is obvious at a glance. Breaking a tough brick feels earned.

**Watch for:** Damage states that are hard to distinguish at the game's scale (zoom the sprites appropriately). Ball bouncing off a damaged brick at weird angles. Multi-hit bricks not awarding the correct score. If level progression is active from Round 1, later levels should use more multi-hit bricks.

---

### Sticky Paddle

A power-up (or a default mode, your call) that makes the ball stick to the paddle on contact instead of bouncing. The ball sits on the paddle and moves with it until the player clicks or presses Space to release. This gives the player time to aim.

If implemented as a power-up, it lasts for 3 catches. A small counter shows remaining catches.

**What good looks like:** The catch feels snappy, not delayed. The ball visually sits on the paddle surface. Releasing the ball feels responsive. The player uses it to aim at specific bricks.

**Watch for:** Ball sticking at the wrong position (offset from where it actually hit). Ball releasing at an unexpected angle. Sticky paddle making the game too easy if it's always active. Interaction with multi-ball: does sticky catch all balls or only the first one?

---

### Combo Scoring

Consecutive brick hits without the ball touching the paddle increase a score multiplier. First brick is 1x, second is 2x, third is 3x, and so on. The combo resets when the ball hits the paddle. Display the current combo count on screen (e.g., "5x COMBO" that grows in size or brightness with the chain).

**What good looks like:** The combo counter creates a tension between playing safe (let the ball come back to aim) and playing aggressive (keep the ball in the bricks for a higher multiplier). The display is satisfying when the combo gets high.

**Watch for:** Combo counter obscuring gameplay. Multiplier making scores absurdly high (cap it or curve it). Combo not resetting correctly when it should. Interaction with multi-ball power-ups: do all balls share one combo counter or does each ball have its own?

---

### Indestructible Bricks

Bricks that the ball bounces off but cannot break. These act as obstacles that shape the play field. Use a visually distinct block sprite or color (e.g., the gold or silver block variant) to make them obviously different from breakable bricks.

Place them strategically to create channels, barriers, or protected areas that make certain bricks harder to reach. The level is complete when all destructible bricks are gone. Indestructible bricks remain.

**What good looks like:** Indestructible bricks change the player's strategy. Bouncing the ball off an indestructible brick to reach a hidden cluster of normal bricks feels clever. They're immediately recognizable as "can't break this."

**Watch for:** Layouts where the ball gets trapped in an infinite bounce loop between indestructible bricks. Indestructible bricks that look too similar to multi-hit bricks (confusing). Layouts that make the level literally impossible. The Power Ball power-up should still bounce off indestructible bricks (they're indestructible, not invisible).

---

### Brick Animations

Bricks are not static. The asset pack includes a 3-frame gloss animation overlay (`assets/pixeltiers-breakout-asset-pack/blocks/gloss_animation/`). Options (pick one or combine):

- **Gloss shimmer:** Overlay the gloss animation frames on bricks as a rolling shimmer that travels across the grid. Each brick catches the shimmer as it passes.
- **Entry animation:** Bricks slide, fade, or drop into position at the start of each level. Stagger by row for a cascade effect.
- **Break animation:** Beyond particles, the brick itself cracks or dissolves over 2 to 3 frames before disappearing. The damage sprites can serve double duty here.

**What good looks like:** The brick grid feels alive. Animations are smooth and don't interfere with collision detection or gameplay timing. The gloss shimmer catches the eye without being distracting.

**Watch for:** Animations that make it unclear whether a brick is still solid (especially during break animations). Entry animations that delay gameplay too long. Shimmer animation causing frame rate drops when applied to many bricks simultaneously.

---

### Level Select

After completing the first playthrough, a level select screen becomes available. The player can replay any previously completed level. Display a thumbnail, title, or number for each level, the player's best score for that level, and whether it was completed.

Level progress can be stored in `localStorage` so it persists between browser sessions.

**What good looks like:** The level select screen feels like a reward for progress. Replaying levels is useful for practicing or improving scores. The pixel font from Round 1 (if implemented) carries through to the level select UI.

**Watch for:** Level select allowing access to unplayed levels. Scores from replayed levels overwriting the campaign score. Navigation between level select and gameplay being confusing.

---

## After You Pick

Pick 3 to 5 features from this menu.

1. Pull the merged Round 1 game and play through it first
2. Write specs for your chosen features with your AI assistant
3. Add features one at a time, playtesting after each
4. Pay attention to how your features interact with Round 1 additions (e.g., do particles still look right with multi-hit bricks? does the speed ramp interact well with power-ups?)
5. Commit after each working feature
6. When satisfied, push your branch and open a PR for review
7. Your reviewer will playtest and either approve or leave feedback
