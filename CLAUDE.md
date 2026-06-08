# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Project Is

Flourish is a **static, single-file HTML prototype** — a clickable wireframe demonstrating the UX of a mobile health app targeting college women. It has no build step, no dependencies, no backend, and no test suite. The entire application lives in `index.html`.

## Running the Prototype

Open directly in a browser:
```bash
open index.html
```

Or serve over HTTP (avoids any browser file:// restrictions):
```bash
python3 -m http.server 8000
# Visit http://localhost:8000
```

## Architecture

### Single-file structure

All HTML, CSS (inline `<style>`), and JavaScript (inline `<script>`) are in `index.html`. There is no compilation, bundling, or asset pipeline.

### Screen navigation

The prototype renders 11 conceptual "screens" as `<div class="screen" id="screen-X">` elements. Only one screen is visible at a time via the `.active` class. Navigation is handled by two global functions:

- `goToScreen(screenId)` — hides all `.screen` elements, adds `.active` to the target, scrolls to top
- `selectOption(element, groupClass)` — toggles `.selected` on option cards within a named group

No state is persisted; selections are purely visual.

### Screen flow

1. Welcome → 2. How It Works → 3–6. Screening questions (eating patterns, body image, stress/emotion, background) → 7. Tier result/program info → 8. Dashboard → 9. Weekly RD check-in → 10. Care Team → 11. Progress

### Design system (CSS variables)

```css
--sage-dark: #2D5A4D
--sage:      #4A7C6F
--sage-light:#5B8A7F
--coral:     #E8A89D
--peach:     #F4B9AA
--cream:     #F5F1E8
--brown:     #C9956F
--gold:      #D4A574
```

The phone frame is 375×812px. A media query at `max-width: 430px` removes the desktop chrome (outer background, rounded corners) so the prototype fills the screen on mobile devices.

### Key CSS patterns

- `.screen { display: none; }` / `.screen.active { display: flex; flex-direction: column; }`
- `.option-card.selected` — highlighted selection state
- Animations: `fadeIn` and `slideUp` keyframes applied to screen entry
- Progress bar uses inline `width` style (e.g., `style="width: 25%"`)
