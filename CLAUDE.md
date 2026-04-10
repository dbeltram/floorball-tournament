# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-file floorball tournament tracker — a self-contained HTML app (`index.html`) with no build step, bundler, or package manager. All HTML, CSS, and JavaScript live in one file.

## Architecture

- **Backend**: Firebase Realtime Database for persistence, Firebase Auth (email/password) for editor access
- **Frontend**: Vanilla JS (ES modules loaded from CDN), no framework
- **State**: A single `state` object holds `players` (array of 12 names) and `fixtures` (keyed match results). Firebase `onValue` listener syncs state in real-time.
- **Auth model**: Read is public, write requires Firebase auth. Authenticated users get `is-editor` class on `<body>`, which toggles editor-only UI via CSS.

## Key Concepts

- **Fixture keys**: Format `{min}_{max}_{leg}` where min/max are player indices. Each pair plays two legs (home/away swapped).
- **Point system**: Win=3, OT/Penalty Win=2, OT/Penalty Loss=1, Loss=0. Draws are only valid with OT+Penalties selected.
- **Penalty goal handling**: When penalties decide a match, the winning penalty goal is included in the displayed score but excluded from GF/GA/GD stats.
- **Standings sort**: Points → Goal Difference → Goals For.

## Development

Open `index.html` directly in a browser or serve with any static server. No build or install needed. Firebase config is hardcoded in the `FIREBASE_CONFIG` constant.
