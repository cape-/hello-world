# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static single-file browser game called **"El Rescate de Manchitas"** — a 20-level 2D platformer written entirely in vanilla HTML/CSS/JavaScript with no build tools, dependencies, or framework.

## Running the Project

Open `index.html` directly in a browser. There is no server, build step, or package manager involved.

## Architecture

Everything lives in `index.html`:

- **CSS** (lines 7–107): Layout for a faux "pink notebook computer" device frame, canvas stage, and on-screen control buttons.
- **Game constants** (lines 199–230): `LEVELS` array defines all 20 levels. Each level object configures obstacles (`gaps`, `balls`, `planes`), teacher behavior (`wakeChance`, `patrol`), and recess mechanics (`recess`).
- **Game state** (lines 236–254): `game` object holds global state (level, keys, recess); `boy` and `teacher` are the two main entity objects.
- **Input handling** (lines 275–311): Unified `press(act, on)` function maps both touch events (`.btn` elements) and keyboard events to game actions.
- **Game loop** (lines 421–538): `update()` runs physics and AI; `render()` (lines 542–867) draws everything imperatively on a `<canvas>` element via the 2D context.
- **Audio** (lines 349–362): Web Audio API oscillators synthesize all sound effects inline — no audio files.

## Key Conventions

- The canvas is fixed at 800×420 logical pixels; CSS scales it to fit the viewport.
- `GROUND = H - 60` (360px) is the shared floor y-coordinate used by all entities.
- Level definitions in `LEVELS` are treated as read-only at runtime — `loadLevel()` always copies obstacle arrays (`balls`, `planes`) before mutating them.
- Teacher modes: `'seated'` (sleeps, may wake), `'patrol'` (walks back and forth with a sight cone), `'chase'` (pursues the player after recess bell).
