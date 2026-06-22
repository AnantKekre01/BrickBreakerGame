# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A browser-based Brick Breaker game built as a single self-contained HTML file (`brickbreaker.html`). No build tools, bundler, or dependencies — just vanilla HTML/CSS/JavaScript with Canvas 2D rendering.

## Workflow

Commit and push to GitHub after every meaningful change. Use clear, descriptive commit messages. Never leave work uncommitted — progress should always be saved to the remote so nothing is lost.

## Running

Open `brickbreaker.html` directly in a browser. No server required.

## Architecture

Everything lives in one file with three sections:

- **CSS** (inline `<style>`) — layout, HUD bar, overlay/menu styling
- **HTML** — HUD (score/level/lives), a `<canvas>` element (780×540), and a start/game-over overlay
- **JavaScript** (inline `<script>`) — game engine using `requestAnimationFrame`

### Game loop structure

`gameLoop()` calls `update()` then `draw()` each frame:

- **`update()`** — moves balls, handles wall/paddle/brick collisions (minimum-overlap method), manages lives/levels, ticks powerups and particles
- **`draw()`** — renders bricks (rounded rects with highlight), paddle (gradient + rounded), balls, powerups, particles, and combo indicator

### Key game constants

Canvas: 780×540. Grid: 6 rows × 13 columns of bricks. Ball speed: 4. Paddle at `y = H - 30`. 5 levels total; levels > 1 give top 2 rows 2 HP.

### State management

Game state is module-level variables (`state`, `score`, `lives`, `level`, `balls[]`, `bricks[]`, `particles[]`, `powerups[]`). States: `'menu'`, `'playing'`, `'gameover'`.

### Power-up system

20% drop chance on brick break. Three types: `wide` (8s duration), `multi` (splits each ball into 3), `slow` (6s duration). Timed powerups revert via `setTimeout`.
