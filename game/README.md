<!--
---
title: "Game"
description: "The Breakout game source and assets"
author: "msp4-don"
date: "2026-05-05"
version: "1.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: game
  - tech: [javascript, html, css, canvas]
---
-->

# Game

The Breakout game lives here. Everything is in `index.html`: HTML structure, CSS styling, and JavaScript game logic. No external dependencies, no build step. Open the file in a browser and play.

---

## 1. Contents

```
game/
├── index.html    # The game (single file, all code embedded)
└── README.md     # This file
```

---

## 2. Running Locally

Open `index.html` directly in a browser, or use the dev server:

```bash
# From the repo root on agents01
./deploy.sh
```

Then visit `https://dev.labby.site` to play.

---

## 3. Conventions

**Single file.** All game code stays in `index.html`. CSS in a `<style>` block, JavaScript in a `<script>` block. This keeps diffs simple and avoids import/build complexity.

**No frameworks.** Vanilla JavaScript, HTML5 Canvas API, Web Audio API. Nothing from npm, no CDN imports.

**No minification.** The code should be readable. Comments are welcome. This is a learning project, not a production deploy.

---

## 4. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory |
| [Baseline Spec](../spec/baseline.md) | Defines what the game must do |
| [Suggestions](../SUGGESTIONS.md) | Feature ideas for future rounds |
| [Tests](../tests/README.md) | Playwright tests that validate the game |
| [deploy.sh](../deploy.sh) | Copies this directory to the nginx dev server |
