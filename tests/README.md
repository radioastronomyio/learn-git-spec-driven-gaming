<!--
---
title: "Tests"
description: "Playwright test suites for the Breakout game"
author: "msp4-don"
date: "2026-05-05"
version: "1.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: testing
  - tech: playwright
---
-->

# Tests

Playwright test suites for the Breakout game. Tests validate gameplay behavior by automating a headless browser: launching the ball, checking brick collisions, verifying score increments, confirming win/lose states. The agent runs these after building a feature to catch regressions before the engineer even opens the game.

---

## 1. Contents

```
tests/
├── *.spec.js         # Playwright test files
└── README.md         # This file
```

---

## 2. Running Tests

From the repo root on agents01:

```bash
npx playwright test
```

Run a specific test file:

```bash
npx playwright test tests/baseline.spec.js
```

Run with the browser visible (headed mode, useful for debugging):

```bash
npx playwright test --headed
```

---

## 3. Test Philosophy

Tests here check playability signals, not code correctness. They verify the same things a human playtester would check, just faster.

Good test assertions:

- "A canvas element exists and has nonzero dimensions"
- "After clicking the canvas, the ball is no longer at its starting position"
- "Breaking a brick increases the score display value"
- "Losing all lives shows a game-over message"

These are observable behaviors, not implementation details. Tests should not reach into JavaScript variables or check internal state. If it's not visible on the canvas or in the DOM, it's not a test target.

---

## 4. Writing New Tests

When adding a feature, add a test that verifies the feature works from a player's perspective. The agent should include test updates as part of the feature spec output.

Test file naming: `feature-name.spec.js` (e.g., `power-ups.spec.js`, `multi-hit-bricks.spec.js`).

A baseline test suite (`baseline.spec.js`) should cover the core game loop from `spec/baseline.md`. Feature tests build on top of it.

---

## 5. Prerequisites

agents01 is expected to have Node.js and Playwright available for test runs. If a fresh checkout does not have local test dependencies yet, install them from the repo root:

```bash
npm init -y
npm install -D @playwright/test
npx playwright install
```

This setup is part of the agents01 infrastructure brief. If tests fail because Playwright is missing on agents01, the infrastructure needs attention before PR approval.

---

## 6. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory |
| [Game](../game/README.md) | The game being tested |
| [Baseline Spec](../spec/baseline.md) | Defines what baseline tests should verify |
| [AGENTS.md](../AGENTS.md) | Requires Playwright tests to pass before PR approval |
