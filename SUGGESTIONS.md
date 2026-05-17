<!--
---
title: "Feature Suggestions"
description: "Backlog of Breakout features for Round 3 and beyond"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: reference
  - domain: [game, specs]
---
-->

# Feature Suggestions

Ideas for making the game better. Pick one, write a spec, hand it to an AI, playtest the result. Each feature is a branch, a PR, and a review.

Features are grouped by game design complexity, not code difficulty. The AI handles implementation; you handle vision.

---

## Visual Polish

Small, self-contained improvements that make the game look and feel better. Good for warming up or for a quick PR.

- Glowing bricks. Bricks emit a soft colored glow that pulses subtly. Different glow colors for different brick types.
- Screen shake. The viewport shakes briefly on paddle impact or when multiple bricks break at once.
- Paddle glow. The paddle glows brighter as a combo chain builds.
- Score pop. When points are earned, a floating number rises from the point of impact and fades out. Combo multiplier text grows with chain length.
- Color themes. Multiple visual themes (neon, retro, ocean, fire) that reskin the game. Swap background, adjust brick colors, change ball trail color.
- Smooth animations. Paddle stretching slightly on hit, ball squishing on bounce.
- Impact sparks. Wall and paddle hits create quick sparks at the contact point so hard redirects feel sharper.
- Animated border. The play area border reacts to danger: dim while calm, brighter when the player is down to the last life.
- Paddle trail. A subtle motion blur or afterimage on the paddle during fast movement.
- Starfield parallax. The background stars shift slightly based on paddle position, adding depth.

---

## Gameplay Mechanics

Features that change how the game plays. Require playtesting to balance.

- Speed zones. Certain areas of the play field speed up or slow down the ball when it passes through.
- Brick formations. Bricks arranged in patterns (diamonds, letters, spirals) instead of a simple grid.
- Moving bricks. Some bricks slide left and right, making them harder to hit.
- Ball magnet. A power-up that gives the paddle a weak magnetic pull on the ball, bending its trajectory slightly.
- Shrinking paddle. The paddle gradually shrinks over time within a level. The grow power-up resets it to full size.
- Brick shields. Some bricks have a one-hit shield (visible as a shimmer) that absorbs the first impact before the brick becomes hittable.
- Ricochet zones. Side walls have angled segments that redirect the ball at unexpected angles.
- Paddle charge shot. Holding the launch button charges the next release, sending the ball faster for a short burst.
- Brick gravity wells. Special bricks pull the ball slightly while they remain on the board, making nearby shots curve.

---

## Power-Up System

Additional power-ups beyond what the asset pack provides. Each one is a small, testable feature. These would need custom sprites or simple shapes.

- Laser paddle. Paddle can shoot upward to break bricks directly. Limited shots.
- Ghost ball. Ball passes through bricks instead of bouncing, breaking everything in its path. Lasts 5 seconds.
- Fireball. Ball ignores brick durability, breaking everything in one hit. Visual fire trail.
- Gravity flip. Bricks fall toward the paddle instead of staying fixed. Lasts until level clears.
- Time freeze. Everything except the paddle freezes for 5 seconds. Reposition freely.
- Aim guide. A short aiming line appears before launch or relaunch, then disappears once the ball is moving.
- Score doubler. Brick points are doubled for a short time, encouraging risky shots while the timer runs.
- Paddle warp. The paddle can instantly jump a short distance left or right once, then the power-up expires.

---

## Physics and Behavior

Features that modify the game's core physics. Require careful tuning.

- Gravity. A constant downward pull on the ball. Changes the entire feel of the game.
- Ball spin. Where the ball hits the paddle affects its curve. Edge hits curve more.
- Wind. A horizontal drift that changes direction periodically. Displayed as a subtle arrow indicator.
- Elastic bricks. Some bricks bounce the ball faster than it arrived. Others absorb energy and slow it down.
- Variable friction. The paddle surface has zones: center returns the ball straight, edges add angle and spin.
- Acceleration. Ball gradually speeds up the longer it stays in play without hitting a brick.
- Portal pairs. Entering one portal sends the ball out of another with its direction preserved.
- Bumper pegs. Round bumpers sit between bricks and rebound the ball with a lively bounce.

---

## Level Design

Features related to how levels are structured and progress.

- Level editor. A simple drag-and-drop interface for placing bricks. Save and load custom levels as JSON.
- Procedural generation. Levels generated algorithmically with increasing complexity. Never the same game twice.
- Boss bricks. Large bricks that take many hits, move, and fire projectiles downward.
- Themed worlds. Groups of 5 levels with a visual theme (space, underwater, forest, volcano). Each world introduces a new mechanic.
- Bonus rounds. Between levels, a timed round with only power-ups and no bricks. Catch as many as you can.
- Endless mode. Bricks regenerate. Score attack with no win condition. Leaderboard.
- Challenge missions. Optional goals: clear a level under a time limit, clear without missing the ball, clear using only edge hits.
- Daily board. One seeded level appears each day so players can compare scores on the same layout.

---

## System Features

Features that affect the game outside of gameplay.

- High scores. Track top 10 scores in localStorage. Display on the title screen.
- Settings menu. Adjustable difficulty (ball speed, paddle size, lives), volume control, theme selector.
- Mobile touch controls. Touch and drag to move the paddle. Tap to launch the ball. Playable on phones.
- Replay system. Record and replay the last completed level. Save replays to share.
- Statistics dashboard. Total bricks broken, games played, average score, longest combo, time played.
- Achievements. "Break 100 bricks in one game," "Complete a level without losing a life," "Collect 5 power-ups in one level." Toast notification on unlock.
- Accessibility options. High-contrast colors, reduced motion, larger ball, and quieter effects toggles.
- Save slots. Keep separate campaign progress for multiple players on the same browser.
- Gamepad support. Controller input for paddle movement and button presses.

---

## Ambitious Projects

Multi-PR features that could span several sessions. Issue-worthy.

- Two-player cooperative. Split the paddle into two halves, each controlled independently. One keyboard, two players.
- AI opponent. A second paddle at the top of the screen controlled by simple AI. Competitive Breakout.
- Level progression campaign. 20+ levels with save/load, unlockable worlds, and a final boss level.
- Mod system. JSON-defined level packs that can be loaded from a URL. Share custom levels.
- Tournament mode. Timed rounds, score comparison, bracket display. For when multiple people want to compete.

---

## How to Use This List

1. Pick a feature that sounds fun
2. Write a spec describing what it should do (in game terms, not code terms)
3. Hand the spec to an AI
4. Playtest the result
5. Commit, PR, review, merge
6. Repeat

If you think of something not on this list, add it. This document grows with the game.
