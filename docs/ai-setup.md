<!--
---
title: "AI Assistant Setup"
description: "How to connect an AI assistant to this project"
author: "radioastronomyio"
date: "2026-05-17"
version: "1.0"
status: "Active"
tags:
  - type: guide
  - domain: [ai-tooling, onboarding]
---
-->

# AI Assistant Setup

The game in this repository is built by an AI from your specs. You describe what you want in game terms; the AI writes the JavaScript. You playtest by opening `game/index.html` in your browser.

This document covers how to connect an AI assistant to the project and what to give it. The specific tool doesn't matter. What matters is that the AI can read your project files and produce code from your specs.

---

## Before You Connect Anything

You cloned this repository from the internet. Before handing its contents to an AI assistant, read through the key files yourself. `AGENTS.md` is the primary instruction document the AI will follow. Read it. Make sure you understand what it tells the AI to do. Check that nothing looks wrong, unexpected, or out of place.

This is a general practice, not specific to this project. Any time you give an AI access to files, know what's in those files first. AI assistants follow instructions they find in their context. Malicious instructions in a cloned repo could cause an AI to produce harmful output, exfiltrate data, or behave in ways you didn't intend.

Read first. Connect second.

---

## What to Give the AI

At minimum, your AI needs:

1. **`AGENTS.md`** as its primary context. This file tells the AI what the project is, where things live, what conventions to follow, and how to work within the spec-driven process.

2. **The spec you're working from.** Start with `spec/baseline.md` for the foundation. When you move to features, give it the relevant feature menu (`spec/round-1-features.md` or `spec/round-2-features.md`).

3. **Access to the project files** so it can read the asset inventory, examine the current game code, and write changes.

The AI does not need every file in the repository at once. Give it what's relevant to the current task. AGENTS.md handles the project-level context; the spec handles the task-level context.

---

## Methods

### Desktop Applications with File Access

Applications like Claude Desktop and the Codex desktop app can access files on your local machine. This is the most natural workflow: the AI reads your project directory, you have a conversation about what to build, and it writes code directly.

**Setup pattern:**

1. Open the application
2. Point it at your project directory (or give it the path)
3. Start a conversation with the baseline spec

Some applications support project-level instructions. If yours does, attach `AGENTS.md` as the project instructions. This means the AI loads the project context automatically at the start of every conversation rather than you pasting it in each time.

| Application | Project instructions feature |
|-------------|------------------------------|
| Claude Desktop / claude.ai | Projects (attach AGENTS.md as project knowledge) |
| ChatGPT | Projects (attach as project file) |
| Gemini | Notebooks (attach as notebook context) |

### Command-Line Tools

CLI-based AI coding tools run in your terminal alongside Git. They can read and write files in your working directory.

Tools in this category include Claude Code, Codex CLI, OpenCode, Gemini CLI, and others. The specific tool changes; the workflow doesn't: you invoke the tool from your project root, give it a spec, and it produces code.

**Setup pattern:**

1. Navigate to your project root in the terminal
2. Run the tool (e.g., `claude`, `codex`, or equivalent)
3. The tool reads the project directory and picks up AGENTS.md (most tools look for it automatically)
4. Describe what you want built

CLI tools are particularly useful for iterating quickly. You can run the tool, review the diff, test in the browser, and loop without leaving the terminal.

### Web-Based (Upload)

If you don't have a desktop application or CLI tool, most AI chat interfaces accept file uploads. This works but requires more manual effort.

**Setup pattern:**

1. Open your AI's web interface (claude.ai, chatgpt.com, gemini.google.com, etc.)
2. Upload `AGENTS.md` and the spec you're working from
3. Describe what you want built
4. Copy the AI's output back into your project files manually

This approach has a higher friction loop (copy-paste instead of direct file writes) but works with any AI that accepts file uploads. It's the fallback when other methods aren't available.

---

## Working With the AI

A few practical notes that apply regardless of which tool you use.

**Spec first, then conversation.** Give the AI the spec document before discussing features. The spec defines the scope. Conversation refines the details.

**Describe behavior, not implementation.** "When the ball hits a brick, the brick disappears and the ball bounces" is a good instruction. "Use a 2D array to track brick state and check collision with AABB" is you doing the AI's job. Let the AI decide how to implement. You decide what the game should do.

**Iterate in game terms.** When something is wrong, describe what you see: "the ball passes through the paddle on the right edge" or "the power-up icon is too small to see while tracking the ball." The AI translates your observation into a code fix. You playtest the fix.

**One feature at a time.** Build the baseline first. Playtest it until it's solid. Then add features from the menu one at a time, playtesting after each. Asking the AI to build everything at once makes debugging harder and learning slower.

**Commit after each working feature.** This creates a clean Git history and gives you rollback points. If a new feature breaks something, you can return to the last working commit.
