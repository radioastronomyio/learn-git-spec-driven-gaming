<!--
---
title: "Assets"
description: "Sprite packs, fonts, music, and reference materials for the game"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: [game, assets]
---
-->

# Assets

Source asset packs for the Breakout game. Everything here is free-licensed for personal and commercial use. When building the game, copy the assets you need into `game/assets/` where the game code references them.

---

## 1. Contents

```
assets/
├── pixeltiers-breakout-asset-pack/   # Sprites: paddles, balls, blocks, power-ups, background
│   ├── paddles/                      # 60 paddle sprites (4 styles × 3 sizes × 5 colors)
│   ├── balls/                        # 120 ball sprites (4 designs × 12 colors, some animated)
│   ├── blocks/                       # 168 block sprites (5 types + 3 damage states × 12 colors)
│   │   └── gloss_animation/          # 3-frame gloss overlay for bricks
│   ├── powerups/                     # 7 power-up types × 4 animation frames
│   ├── background.png                # Star sky background (full resolution)
│   ├── background-400.png            # Star sky background (400px)
│   ├── spritesheet_assets.png        # All sprites on one sheet
│   └── spritesheet_assets_preview.png
├── fonts/                            # Pixel fonts
│   ├── opf-large.ttf                 # Owlish Pixel Font, large variant
│   ├── opf-medium.ttf                # Owlish Pixel Font, medium variant
│   ├── opf-small.ttf                 # Owlish Pixel Font, small variant
│   ├── pixbob-lite.ttf               # Pixbob font, lite weight
│   └── pixbob-tall lite.ttf          # Pixbob font, tall lite weight
├── music/                            # Music loops (.ogg)
│   ├── *-sf-action-1.ogg             # Gameplay loop 1
│   ├── *-sf-action-2.ogg             # Gameplay loop 2
│   ├── *-sf-title-menu-credit.ogg    # Title/menu loop
│   ├── *-sf-explo-1.ogg              # Stinger 1
│   ├── *-sf-explo-2.ogg              # Stinger 2
│   └── *-sf-explo-3.ogg              # Stinger 3
├── cosmic-breakout-html-game-template-free/  # Reference: complete breakout (MIT)
│   ├── index.html                    # Single-file game with procedural audio
│   ├── readme.md
│   └── license.txt
└── README.md                         # This file
```

---

## 2. Licenses

| Pack | Author | License | Link |
|------|--------|---------|------|
| Pixeltier's Breakout Asset Pack | pixeltier (Sascha Naderer) | Free for personal and commercial use. May not be redistributed or resold. | [itch.io](https://pixeltier.itch.io/breakout-game-assets) |
| Owlish Pixel Fonts | Owlish | Free | [itch.io](https://owlishpixel.itch.io/) |
| Pixbob Lite | Pixbob | Free (lite version) | [itch.io](https://pixbob.itch.io/) |
| Torone Loop Pack 02 | Torone | Royalty-free | See download source |
| Cosmic Breakout Template | Community | MIT | See `cosmic-breakout-html-game-template-free/license.txt` |

---

## 3. Using Assets in the Game

Assets in this directory are the source of truth. The game code in `game/index.html` references assets from `game/assets/`, not from here. Part of the build process is selecting which assets to copy over.

**Baseline requires:** one paddle sprite, one ball sprite, 5+ block color variants, and the star background.

**Round 1 adds:** pixel fonts (if Score Display Polish is chosen), music loops (if Background Music is chosen).

**Round 2 adds:** power-up sprites (4-frame animations), damage-state block sprites, large paddle variants (for the grow power-up).

Only copy what you need. The full pack is large; the game directory should contain only the assets actively in use.

---

## 4. Conventions

- Filenames: lowercase, hyphenated. The Pixeltier pack files are already lowercase after the rename pass.
- Formats: PNG for sprites, TTF/OTF for fonts, OGG for audio.
- Rendering: Pixel art sprites should be displayed at integer scale with nearest-neighbor interpolation (`imageSmoothingEnabled = false` in Canvas 2D).

---

## 5. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory |
| [AGENTS.md](../AGENTS.md) | AI context, references the asset inventory |
| [Baseline Spec](../spec/baseline.md) | Defines which assets the baseline requires |
