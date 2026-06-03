🌿 Grove Focus

### *Pomodoro · Music · Tasks · Habits*

A warm, single-file productivity app — Pomodoro timer, Spotify embed, task manager, and habit tracker all in one pure HTML/CSS/JS file.


[✦ Features](#-features) · [✦ Modules](#-modules) · [✦ Design System](#-design-system) · [✦ Getting Started](#-getting-started) · [✦ Customise](#-customisation)

</div>

---

## 📖 Overview

Grove Focus is a **single-file productivity app** with a nature-warm aesthetic. It combines a full-featured Pomodoro timer, task list, habit tracker, Spotify music embed, and daily quotes into one zero-dependency `index.html`. Everything persists across sessions via `localStorage`.

---

## ⚡ Quick Start

```bash
git clone https://github.com/your-username/grove-focus.git
cd grove-focus
open index.html       # macOS
# or double-click index.html on Windows / Linux
```

> No npm. No config. No build step. Works straight from the file system.

---

## ✨ Features

### ⏱️ Pomodoro Timer
| Feature | Detail |
|---|---|
| 3 Modes | Focus · Short Break · Long Rest |
| SVG Ring | Animated gradient progress ring (stroke-dashoffset) |
| Custom Durations | Editable minute inputs for all 3 modes |
| Auto-advance | Automatically switches modes on completion |
| Audio Chime | Web Audio API chord (C5 · E5 · G5 · C6) plays on session end |
| Session Dots | Visual row of dots tracks completed sessions |
| Session Label | Shows current session number within the 4-session cycle |

### ✅ Task Manager
| Feature | Detail |
|---|---|
| Add / Complete / Delete | Full CRUD, `Enter` key supported |
| Persistent | Saved to `localStorage` as `grove-tasks` |
| Remaining Count | Live "X left" counter updates on every action |

### 🔥 Habit Tracker
| Feature | Detail |
|---|---|
| Add / Delete Habits | Custom daily habits with names |
| Streak Counter | 🔥 streak increments each day the habit is checked |
| Daily Reset | "Reset today" button un-checks all habits for the day |
| Persistent | Saved to `localStorage` as `grove-habits` |
| Date-aware | Automatically resets state when a new day is detected |

### 🎵 Spotify Embed
| Feature | Detail |
|---|---|
| URL Parsing | Parses any `open.spotify.com` share link |
| Supported Types | Tracks · Albums · Playlists · Podcasts · Episodes |
| Adaptive Height | 152px for tracks/episodes, 232px for playlists/albums |
| Dark Theme | Embeds use Spotify's dark iframe theme |

### 📊 Progress Tracking
| Feature | Detail |
|---|---|
| Daily Session Count | Counts focus sessions completed today |
| Adjustable Goal | Input to set daily session target (default: 8) |
| Segment Bar | One coloured segment per completed session |
| Flower Viz | 🌿 icons that "bloom" as sessions are completed |
| Percentage | Live "X% complete" toward daily goal |

### 💬 Quote Card
| Feature | Detail |
|---|---|
| 15 Curated Quotes | Deep work, productivity, and focus themed |
| Cycle Button | "↻ new" cycles to the next quote |
| Random Start | Opens on a random quote each session |

### 🎨 UI & UX
| Feature | Detail |
|---|---|
| Dark / Light Mode | Toggle persists to `localStorage` |
| Toast Notifications | Auto-dismiss messages for all key events |
| Animated Blobs | 3 blurred background colour blobs |
| Paper Texture | SVG `feTurbulence` noise overlay for depth |
| Scroll Animations | `fadeDown` + `fadeUp` on page load |
| Responsive | Single-column layout at ≤ 680px |

---

## 🗂️ Modules

| Card | ID / Location | Persists |
|---|---|---|
| Timer | `.timer-card` (left column, spans 2 rows) | Session count in `grove-state` |
| Quote | `.quote-inner` (right col, top) | — |
| Tasks | `.task-inner` (right col, mid) | `grove-tasks` |
| Spotify | `.spotify-inner` (right col, bottom) | — |
| Progress | `.prog-inner` (bottom left) | `grove-state` |
| Habits | `.habit-inner` (bottom right) | `grove-habits` |

---

## 📁 Project Structure

```
grove-focus/
├── index.html          ← Everything — HTML + CSS + JS in one file
│   ├── <style>         ← CSS variables, layout, all component styles, dark mode
│   ├── <body>          ← App shell: header, main-grid, bottom-grid, toast
│   └── <script>        ← Quotes, Spotify parser, Timer, Tasks, Habits, Theme, Chime
│
└── README.md
```

---

## 🎨 Design System

### Colour Palette

| Token | Hex | Swatch | Usage |
|---|---|---|---|
| `--cream` | `#f2ede0` | ![#f2ede0](https://img.shields.io/badge/-%23f2ede0-f2ede0?style=flat-square) | Page background |
| `--paper` | `#f7f2e6` | ![#f7f2e6](https://img.shields.io/badge/-%23f7f2e6-f7f2e6?style=flat-square) | Card background |
| `--terra` | `#c04a1e` | ![#c04a1e](https://img.shields.io/badge/-%23c04a1e-c04a1e?style=flat-square) | Primary / active / timer |
| `--moss` | `#2e5e28` | ![#2e5e28](https://img.shields.io/badge/-%232e5e28-2e5e28?style=flat-square) | Habit tracker / done |
| `--bark` | `#1a0e08` | ![#1a0e08](https://img.shields.io/badge/-%231a0e08-1a0e08?style=flat-square) | Headings / ring track |
| `--ink` | `#1a0e08` | ![#1a0e08](https://img.shields.io/badge/-%231a0e08-1a0e08?style=flat-square) | Body text |

### Typography

```
Display / Headings  →  Fraunces     weights: 300, 500, 700  (italic variants)
Monospace / Labels  →  DM Mono      weights: 300, 400
```

### Ring Gradient

```css
/* SVG linearGradient — id="sg" */
stop 0%   → #c04a1e   (terra)
stop 50%  → #d96030   (terra2)
stop 100% → #2e5e28   (moss)
```

### Dark Mode

Dark mode is applied via `body.dark` class. All tokens are overridden inside that selector:

```css
body.dark {
  --cream: #161009;
  --paper: #1a1108;
  --ink:   #f0e6d6;
  /* ... all other tokens remapped to dark equivalents */
}
```

---

## 📐 Responsive Layout

```
Desktop  →  > 680px    2-col main grid + 2-col bottom grid
Mobile   →  ≤ 680px    Single column, all cards stacked vertically
```

---

## 💾 localStorage Keys

| Key | Type | Contents |
|---|---|---|
| `grove-state` | JSON object | `{ pomosToday, sessCompleted, goal, date }` |
| `grove-tasks` | JSON array | `[{ text, done }]` |
| `grove-habits` | JSON array | `[{ id, name, streak, lastDone }]` |
| `grove-dark` | String | `"1"` (dark) or `"0"` (light) |

> All keys are read on page load and reset automatically when `date` doesn't match today's date.

---

## 🔧 Customisation

<details>
<summary><strong>⏱️ Change default timer durations</strong></summary>
<br/>

Edit the HTML input `value` attributes:

```html
<input type="number" id="fMin" value="25" min="1" max="90">  <!-- Focus -->
<input type="number" id="sMin" value="5"  min="1" max="30">  <!-- Short break -->
<input type="number" id="lMin" value="15" min="1" max="60">  <!-- Long rest -->
```

</details>

<details>
<summary><strong>💬 Add or edit quotes</strong></summary>
<br/>

Edit the `QUOTES` array in the `<script>` block:

```js
const QUOTES = [
  { text: "Your quote here.", author: "Author Name" },
  // ...
];
```

</details>

<details>
<summary><strong>🎵 Change the completion chime</strong></summary>
<br/>

Edit the frequency array in `playChime()`:

```js
// [frequency Hz, delay seconds]
[[523.25, 0], [659.25, .2], [783.99, .4], [1046.5, .65]]
// C5        E5            G5            C6
```

Replace with any frequencies for a different chord or melody.

</details>

<details>
<summary><strong>🎨 Adjust the colour palette</strong></summary>
<br/>

Edit the `:root` block at the top of `<style>`:

```css
:root {
  --terra: #c04a1e;   /* ← primary accent */
  --moss:  #2e5e28;   /* ← habits / success */
  --cream: #f2ede0;   /* ← page background */
  --paper: #f7f2e6;   /* ← card background */
}
```

Dark mode tokens are in `body.dark { ... }` just below.

</details>

<details>
<summary><strong>🌿 Change the progress flower icon</strong></summary>
<br/>

Find this line in `updateProgress()` inside the `<script>` block:

```js
f.textContent = '🌿';   // ← swap for any emoji: 🌸 ⭐ 🍕 🔥
```

</details>

---

## 🙌 Credits

| Resource | Usage |
|---|---|
| [Google Fonts](https://fonts.google.com) | Fraunces & DM Mono typefaces |
| [Spotify Embed API](https://developer.spotify.com/documentation/embeds) | Music player iframe |
| [Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) | Completion chime (native browser) |

---

## 📄 License

This project is licensed under the **MIT License** — free to use, fork, and build upon.

---

<div align="center">

Built for deep work & daily ritual &nbsp;·&nbsp; **Grove Focus © 2025**

</div>
