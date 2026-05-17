# Cosmic Breakout — HTML Game Template

A polished, single-file HTML5 brick breaker (Arkanoid-style) with **multi-ball physics**, **boss bricks**, **10 power-ups**, **6 procedural level patterns**, **combos**, and a striking **deep-space nebula aesthetic** rendered procedurally — no external assets.

Drop the file on any web host (or itch.io) and it just works — no build step, no dependencies, no images, no audio files.

## Features

### Visual style
- 🌌 **Procedural cosmic nebula** — pre-rendered 1024×1024 nebula tile with 6 large soft radial gradients in purple/pink/cyan, drawn once and tiled+wrapped at runtime
- ⭐ **Two-layer parallax starfield** — 240 small stars + 80 larger glowing stars on separate offscreen canvases, scrolling at different speeds for true depth
- ✨ **Glowing crystalline bricks** — gradient-filled rounded rectangles with `shadowBlur` glow, inner highlights, crack lines on damaged bricks
- 🔮 **Energy-orb ball** — radial-gradient core with a soft cyan halo and trailing particles
- 💎 **Sleek paddle** — gradient cyan pill with white core pip, glow halo, special indicators (laser triangles, sticky ring)
- 🌠 **Particle-rich shatter effects** — every brick break scatters glowing color-matched debris

### Gameplay
- 🏓 **Smooth paddle physics** — drag (mobile/mouse), keyboard (A/D/←/→), gamepad stick. Hit position controls bounce angle (max 72°).
- ⚡ **Realistic ball physics** — AABB-circle collision with proper face-normal reflection, speed acceleration over time, multi-ball up to 8 at once
- 🧱 **6 brick types**:
  - **Standard** (cyan, 1 HP, 10pts)
  - **Tough** (purple, 2 HP, 25pts)
  - **Reinforced** (pink, 3 HP, 50pts)
  - **Explosive** (red ⚠, chains to neighbors, 30pts)
  - **Mystery** (yellow ?, always drops a power-up, 35pts)
  - **Boss** (gold, 8+ HP scaling, drops 3 power-ups + big score)
- 💊 **10 power-ups** that fall from broken bricks:
  - **Multi-Ball** ×3 — spawns 2 extra balls
  - **Wide Paddle** ⬌ — 50% wider for 15s
  - **Sticky** ◉ — ball sticks on next hit, click to release
  - **Laser** ⚡ — paddle fires lasers when clicked, 10s
  - **Slow** 🐢 — ball at 65% speed, 10s
  - **+Life** ♥ — extra life
  - **Score×2** — double scoring, 15s
  - **Big Ball** ⊙ — 1.7× ball size, 10s
  - **Narrow** ⬍ (bad) — paddle shrinks 60%, 10s
  - **Fast** » (bad) — ball at 135% speed, 8s
- 🗺 **6 procedural level patterns** — Wall / Pyramid / Fortress / Scattered / Stripes / Boss Room. Boss every 5th level. HP scales per level.
- 🔥 **Combo system** — chain bricks without losing a ball for a 1× → 6× score multiplier. "COMBO N!" bursts at 10/25/50/100/200.
- ❤ **Lives** — start with 3, max 5, +1 every 5000 score
- 🎯 **Score×2 stacking with combo** — top combos can yield 12× scores

### Polish & UX
- 📊 **Master CONFIG block** at the top of the script — every value retunable in seconds
- 🎵 **Procedural Web Audio** — 17 SFX synthesized at runtime, zero audio files
- ⚙ **Full settings menu** — Volume, SFX mute, Performance (high/low), Screen Shake, Score Popups, Drag Sensitivity
- 💾 **Persistent stats** — best score, best level, best combo, total bricks, total power-ups, runs played
- 🎮 **Universal input** — keyboard, mouse drag, touch drag, full gamepad support with menu navigation
- 📱 **Mobile-first** — clamp() responsive sizing, `env(safe-area-inset-*)` notch handling, DPR capped at 2
- ⚡ **Object pooling** + **low-perf mode** for steady 60fps on phones
- 🎯 **Premium HUD** — minimal when nothing's happening, only shows what's relevant
  - Lives top-left (heart icons fade as you lose them)
  - Score top-center pill with best score below
  - Level + bricks-left top-right
  - Combo meter mid-left (only ≥3)
  - Power-up timer pills right side
  - Pause button bottom-left
  - Action button bottom-right (Launch / Fire)
  - Level transition banner ("LEVEL N" full-screen)

## File structure

```
index.html      (single-file game — open it directly in a browser)
README.md       (this file)
LICENSE.txt     (MIT)
```

## Itch.io listing fields

When uploading, use these settings:

| Field | Value |
|---|---|
| Classification | Game assets > Templates |
| Kind of project | HTML |
| File type | Source code |
| Pricing | Pay what you want, $0 minimum, $2 suggested |
| Embed | 720×1080 (portrait) or 960×600 (landscape), mobile friendly ✓, fullscreen ✓, autostart ✗ |
| AI disclosure | Yes, code/text only (no AI graphics or sounds — all procedural) |
| Custom noun | "template" |

**Suggested tags** (10 max): `template`, `html5`, `source-code`, `breakout`, `arkanoid`, `brick-breaker`, `arcade`, `mobile`, `casual`, `free`

## Architecture (script sections)

| # | Section | Purpose |
|---|---|---|
| 1 | MASTER CONFIG | Every retunable value in one block |
| 2 | UTILITIES | rand, lerp, clamp, weighted picker, number formatter |
| 3 | PRE-RENDERED ASSETS | Nebula tile + 2 starfield tiles built once at startup |
| 4 | AUDIO | Procedural Web Audio with per-SFX volume map |
| 5 | SETTINGS | localStorage persistence |
| 6 | STATS | Cross-run best score / level / combo / bricks / power-ups / runs |
| 7 | INPUT | Keyboard + touch + mouse + gamepad with pointer-position tracking |
| 8 | OBJECT POOL | Generic Pool class |
| 9 | PARTICLES | FX system with optional glow + low-perf scaling |
| 10 | SCORE POPUPS | Floating numbers + COMBO bursts |
| 11 | BRICK TYPES | 6 brick definitions (Standard / Tough / Reinforced / Explosive / Mystery / Boss) |
| 12 | POWERUP TYPES | 10 power-up definitions, weighted picker |
| 13 | LEVEL GENERATOR | 6 procedural patterns, difficulty scaling per level |
| 14 | GAME class | Owns runtime state, update/draw, ball-brick collision math |
| 15 | BOOTSTRAP | UI wiring, main loop |

## Visual style — how it's built

The look comes from a few specific techniques. Anyone customizing the template should know these:

### Pre-rendered nebula tile
Built once in `buildNebulaTile()` as a 1024×1024 offscreen canvas:
1. Linear gradient base from `#05051a` → `#0a0a25` → `#0d0830`
2. 6 soft radial-gradient color clouds in purple/pink/cyan, blended with `globalCompositeOperation = 'screen'` for additive light glow

The main loop tiles this canvas across the screen, scrolling slowly with `bgScroll * 0.15`. Pre-rendering avoids creating expensive radial gradients per frame.

### Two-layer starfield
Each layer is a 1024×1024 offscreen canvas drawn once at startup. Each star is a glowing radial gradient + a bright core. Stars never twinkle (saves perf) but parallax scroll at different rates (`0.4` and `0.7` of the bg scroll speed) to create depth.

### Glowing bricks
Each brick uses Canvas's `shadowBlur` for a real glow halo, plus a vertical gradient (highlight → base → shadow) for a 3D crystalline feel. Damaged bricks (HP > 1) get black crack lines that increase as HP drops. Boss bricks have a mini HP bar at the bottom and "BOSS" text overlay.

### Energy-orb ball
Two layers per ball:
1. **Outer halo**: large radial gradient from white → cyan → transparent, drawn at 3× ball radius
2. **Core**: small radial gradient with offset highlight (white → cyan → deep cyan) at actual radius

This creates the bright "energy ball" look — much cheaper than a real WebGL bloom shader.

### Particle trail
Every ball emits one cyan particle every 12ms with `glow: true`. Particles fade and decay naturally. No per-frame trail lookup needed — just timed emission.

### Combat-feel polish
- Camera shake on every brick hit (small) and every paddle hit (smaller)
- Brick flash white on hit (with fade)
- Ball speeds up slightly with each brick to keep tension growing

## Quick recipes

### Add a new brick type
Append to `BRICK_TYPES` in section 11 with a unique `id`:
```js
{ id:'rainbow', label:'RBW', color:'#fff', glow:'#a855f7', hp:5, score:100, weight:3 },
```
Then in `damageBrick()` or `destroyBrick()`, add custom behavior with `if(br.type === 'rainbow') { ... }`.

### Add a new power-up
Append to `POWERUP_TYPES` in section 12:
```js
{ id:'fireball', label:'🔥', color:'#fb923c', glow:'#ea580c', weight:8, bad:false },
```
Then in `activatePowerup()`, add the activation logic. To make it timed, add a `runState.fireballUntil` field and check against `gameTime`.

### Adjust ball speed
All in `CONFIG.ball`:
- `baseSpeed`: starting speed
- `maxSpeed`: cap
- `speedupPerBrick`: bump on each brick hit
- `speedupPerSecond`: continuous accel over time

### Tune difficulty
- `CONFIG.brick.cols` / `rows` — initial grid size
- `CONFIG.level.bricksAddedPerLevel` — extra bricks per level
- `CONFIG.level.hpScalePerLevel` — HP bonus scaling
- `CONFIG.level.bossEvery` — N levels between bosses

### Change ball color
In `drawBalls()`, change the gradient colors for the halo and core. Default is white→cyan, but blue/pink/green all work great.

### Change paddle color
In `CONFIG.paddle.color/coreColor/glowColor` plus the `drawPaddle()` gradient stops. Match to your theme.

### Reskin ideas

- **Frost Breakout** — change nebula tile to icy blue/white blobs, stars become snowflakes (slightly slower particles, larger glow), bricks become ice crystals (cyan/white), ball stays white
- **Lava Breakout** — nebula becomes orange/red with magma swirls, bricks become molten rock chunks, ball becomes a fireball (orange→yellow gradient), paddle becomes obsidian black
- **Forest Breakout** — nebula becomes deep forest green with mossy spots, stars become fireflies (yellow/green), bricks become wooden logs (brown gradient), ball becomes an axe-glow
- **Underwater Breakout** — nebula becomes ocean-blue with abyssal dark spots, stars become bioluminescent dots, bricks become coral/treasure chests
- **Glitch Breakout** — nebula becomes black with horizontal RGB shift bands, stars become random pixels, bricks become digital blocks with glitch artifacts (random pixel shifts)

## Performance

- 60 FPS on mid-tier phones with default settings, tested with 100+ bricks + 8 multi-balls + active particles
- **Performance: LOW** in settings cuts particle counts to 40% — bumps perf significantly without changing gameplay feel
- Pre-rendered nebula and starfield tiles mean the background is just a few `drawImage` calls per frame instead of hundreds of `arc()` and `createRadialGradient()` calls
- DPR capped at 2 to avoid wasting fillrate on retina pixels
- Object pooling for balls, bricks, power-ups, lasers, particles, score popups — zero GC pressure during gameplay

## Browser support

Tested on modern Chrome / Safari / Firefox / Edge. Uses standard Canvas 2D, Web Audio, GamepadAPI, localStorage. No WebGL.

## Controls reference

| Action | Keyboard | Touch | Mouse | Gamepad |
|---|---|---|---|---|
| Move paddle | A/D, ←/→ | Drag | Drag | Left stick |
| Launch ball / Fire laser | Space / Enter | Tap or Action button | Click or Action button | A |
| Pause | Esc / P / K | Pause button | Pause button | Start |
| Menu navigate | W/S, ↑/↓ | Tap | Click | D-pad / stick |
| Confirm | Enter / Space | Tap | Click | A |
| Back | Esc / Backspace | Tap Back | Click Back | B |

## LocalStorage keys

- `cosmic_breakout_settings_v1` — user preferences
- `cosmic_breakout_stats_v1` — best score, level, combo, totals

## License

MIT — use it for personal or commercial games. See LICENSE.txt.

## Credits

Made with ☕ as a starter template. All visuals (nebula, starfield, bricks, ball, paddle, power-ups) are procedurally generated. All audio is synthesized at runtime. No external assets.

Have fun breaking the cosmos!
