---
name: svg-icon-generator
description: >
  Generate clean, scalable SVG icons on demand. Triggers when the user asks
  for an icon, logo mark, symbol, or SVG graphic. Produces production-ready
  SVG code following best practices for accessibility, scalability, and reuse.
triggers:
  - svg icon
  - icon generator
  - create icon
  - make icon
  - draw icon
  - svg logo
  - svg symbol
  - vector icon
---

# SVG Icon Generator Skill

## Purpose

Generate clean, accessible, production-ready SVG icons from natural language
descriptions. This skill covers everything from simple flat icons to more
detailed illustrated marks.

---

## Core Principles

1. **Always use a square viewBox** — default to `viewBox="0 0 24 24"` (24×24)
   for UI icons, `viewBox="0 0 64 64"` for larger illustrative icons.
2. **No hardcoded width/height** on the `<svg>` element — let the consumer
   control size via CSS.
3. **Use `currentColor`** for stroke/fill so icons inherit color from their
   context.
4. **Accessible by default** — include `role="img"` and a `<title>` element.
5. **Minimal, clean paths** — prefer geometric primitives (`<circle>`,
   `<rect>`, `<path>`, `<polyline>`) over overly complex path data.
6. **Consistent stroke width** — use `stroke-width="2"` for 24px icons,
   `stroke-width="3"` for 16px icons, `stroke-width="1.5"` for 32px+ icons.
7. **No inline styles** — use SVG presentation attributes only.

---

## Icon Style Presets

### Outline (default)
- `fill="none"`, `stroke="currentColor"`, `stroke-width="2"`
- `stroke-linecap="round"`, `stroke-linejoin="round"`
- Best for: UI icons, navigation, toolbars

### Solid / Filled
- `fill="currentColor"`, `stroke="none"`
- Best for: badges, status indicators, buttons

### Duotone
- Two layers: a base shape at `opacity="0.3"` + a detail layer at full opacity
- Both use `fill="currentColor"`
- Best for: feature illustrations, empty states

### Two-Color
- Primary shape uses `fill="currentColor"`
- Accent shape uses `fill="var(--icon-accent, #6366f1)"` or a second passed color
- Best for: branded icons, product illustrations

---

## Standard Template

```svg
<svg
  xmlns="http://www.w3.org/2000/svg"
  viewBox="0 0 24 24"
  fill="none"
  stroke="currentColor"
  stroke-width="2"
  stroke-linecap="round"
  stroke-linejoin="round"
  role="img"
  aria-labelledby="icon-title"
>
  <title id="icon-title">Icon description here</title>
  <!-- paths here -->
</svg>
```

---

## Common Icon Patterns & Geometry

### Arrows
- Right arrow: `<polyline points="9 18 15 12 9 6"/>`
- Left arrow: `<polyline points="15 18 9 12 15 6"/>`
- Down arrow: `<polyline points="6 9 12 15 18 9"/>`
- Up arrow: `<polyline points="6 15 12 9 18 15"/>`
- With shaft: add `<line x1="5" y1="12" x2="19" y2="12"/>` behind the chevron

### Navigation / UI
- Hamburger menu: three `<line>` elements at y=6, y=12, y=18
- Close (X): `<line x1="18" y1="6" x2="6" y2="18"/>` + `<line x1="6" y1="6" x2="18" y2="18"/>`
- Plus: `<line x1="12" y1="5" x2="12" y2="19"/>` + `<line x1="5" y1="12" x2="19" y2="12"/>`
- Search: `<circle cx="11" cy="11" r="8"/>` + `<line x1="21" y1="21" x2="16.65" y2="16.65"/>`

### Status / Feedback
- Check: `<polyline points="20 6 9 17 4 12"/>`
- Alert triangle: `<path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/>` + dot + line
- Info circle: `<circle cx="12" cy="12" r="10"/>` + `<line x1="12" y1="8" x2="12" y2="12"/>` + `<line x1="12" y1="16" x2="12.01" y2="16"/>`

### Files & Data
- File: `<path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V9z"/>` + `<polyline points="13 2 13 9 20 9"/>`
- Folder: `<path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/>`

### People & Social
- User: `<path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>` + `<circle cx="12" cy="7" r="4"/>`
- Users: above pattern shifted left + second partial silhouette on right

### Nature & Objects
- Star: `<polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>`
- Heart: `<path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/>`

---

## Background Shape Primitives

These basic shapes are building blocks for icon backgrounds, badges, containers,
and layered compositions. Use them behind a symbol/glyph to create framed icons
(e.g. a camera icon inside a rounded square, a lock inside a shield).

### Circle
Full circle — great for avatars, dot indicators, and pill badges.
```svg
<!-- Filled -->
<circle cx="12" cy="12" r="10" fill="currentColor"/>

<!-- Outline -->
<circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/>

<!-- Soft background (low opacity) -->
<circle cx="12" cy="12" r="10" fill="currentColor" opacity="0.12"/>
```
**Variants:**
- Small dot: `r="3"` centered
- Ring: outline circle + slightly smaller filled circle cut out via `fill-rule`
- Doughnut: two concentric circles (outer filled, inner `fill="white"` or use `clip-path`)

### Rectangle & Square
Use `<rect>` for card backgrounds, button shapes, and grid tiles.
```svg
<!-- Square (no rounding) -->
<rect x="2" y="2" width="20" height="20" fill="currentColor"/>

<!-- Rounded square — most common for app icons -->
<rect x="2" y="2" width="20" height="20" rx="4" ry="4" fill="currentColor"/>

<!-- Squircle-like (heavy rounding) -->
<rect x="2" y="2" width="20" height="20" rx="8" ry="8" fill="currentColor"/>

<!-- Wide rectangle / banner -->
<rect x="1" y="6" width="22" height="12" rx="2" fill="currentColor"/>

<!-- Soft background -->
<rect x="2" y="2" width="20" height="20" rx="5" fill="currentColor" opacity="0.12"/>
```
**Tips:**
- `rx` equal to half the width/height gives a pill/capsule shape
- Pair with `stroke` + `fill="none"` for an outline badge frame
- Use `rx="6"` as a default for modern "squarish" app icon backgrounds

### Triangle
SVG has no `<triangle>` element — use `<polygon>` or `<path>`.
```svg
<!-- Equilateral triangle pointing up (centred in 24×24) -->
<polygon points="12,3 22,21 2,21" fill="currentColor"/>

<!-- Outline only -->
<polygon points="12,3 22,21 2,21"
  fill="none" stroke="currentColor" stroke-width="2"
  stroke-linejoin="round"/>

<!-- Pointing down -->
<polygon points="2,3 22,3 12,21" fill="currentColor"/>

<!-- Pointing right (play-button style) -->
<polygon points="5,3 19,12 5,21" fill="currentColor"/>

<!-- Pointing left -->
<polygon points="19,3 5,12 19,21" fill="currentColor"/>

<!-- Rounded triangle (via path) -->
<path d="M12 4 L21.5 20 Q22 21 21 21 H3 Q2 21 2.5 20 Z"
  fill="currentColor" stroke-linejoin="round"/>
```
**Tips:**
- For softer corners on `<polygon>`, switch to `<path>` with quadratic curves at each vertex
- A small downward triangle (`▾`) works well as a dropdown indicator behind a caret icon

### Diamond / Rotated Square
```svg
<!-- Diamond centred in 24×24 -->
<polygon points="12,2 22,12 12,22 2,12" fill="currentColor"/>

<!-- Outline diamond -->
<polygon points="12,2 22,12 12,22 2,12"
  fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
```

### Hexagon
Popular for avatar frames and tech/data iconography.
```svg
<!-- Flat-top hexagon -->
<polygon points="12,2 21.39,7 21.39,17 12,22 2.61,17 2.61,7"
  fill="currentColor"/>

<!-- Outline -->
<polygon points="12,2 21.39,7 21.39,17 12,22 2.61,17 2.61,7"
  fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
```

### Shield
Common for security, trust, and protection icons.
```svg
<path d="M12 2 L20 5.5 V11 C20 15.4 16.5 19.4 12 21 C7.5 19.4 4 15.4 4 11 V5.5 Z"
  fill="currentColor"/>

<!-- Outline shield -->
<path d="M12 2 L20 5.5 V11 C20 15.4 16.5 19.4 12 21 C7.5 19.4 4 15.4 4 11 V5.5 Z"
  fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"/>
```

---

## Combining Backgrounds with Foreground Icons

Layer a background shape behind a glyph using SVG stacking order (first element
renders bottom-most). Use `opacity` or a lighter fill on the background to keep
the foreground readable.

```svg
<!-- Example: lock icon on a rounded-square background -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" role="img">
  <title>Secure</title>

  <!-- Background -->
  <rect x="2" y="2" width="20" height="20" rx="5"
    fill="currentColor" opacity="0.15"/>

  <!-- Foreground icon -->
  <rect x="8" y="11" width="8" height="7" rx="1"
    fill="none" stroke="currentColor" stroke-width="2"/>
  <path d="M8 11V8a4 4 0 0 1 8 0v3"
    fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
</svg>
```

**Combination recipes:**
| Background | Best foreground uses |
|---|---|
| Filled circle | Single-glyph monogram, status dot, avatar placeholder |
| Rounded rect (rx=4–6) | App icons, action buttons, tool icons |
| Heavy rounded rect (rx=8+) | iOS-style app icons, feature tiles |
| Shield | Security, auth, privacy icons |
| Hexagon | Data, tech, infrastructure icons |
| Diamond | Alert/warning, premium/special tier icons |
| Triangle | Directional, play/media, warning contexts |

---

## Gradients

SVG gradients are defined once in `<defs>` and referenced by `id`. Keep them
simple — one or two stops is almost always enough for icons.

### Linear Gradient
Flows in a straight line between two points.
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
  <defs>
    <!-- Top to bottom (default) -->
    <linearGradient id="grad-tb" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#6366f1"/>
      <stop offset="100%" stop-color="#8b5cf6"/>
    </linearGradient>

    <!-- Left to right -->
    <linearGradient id="grad-lr" x1="0" y1="0" x2="1" y2="0">
      <stop offset="0%" stop-color="#06b6d4"/>
      <stop offset="100%" stop-color="#3b82f6"/>
    </linearGradient>

    <!-- Diagonal (top-left to bottom-right) -->
    <linearGradient id="grad-diag" x1="0" y1="0" x2="1" y2="1">
      <stop offset="0%" stop-color="#f59e0b"/>
      <stop offset="100%" stop-color="#ef4444"/>
    </linearGradient>
  </defs>

  <!-- Apply to any shape -->
  <rect x="2" y="2" width="20" height="20" rx="5" fill="url(#grad-tb)"/>
</svg>
```

### Radial Gradient
Radiates outward from a centre point — good for glows and depth effects.
```svg
<defs>
  <radialGradient id="grad-radial" cx="50%" cy="50%" r="50%">
    <stop offset="0%" stop-color="#a78bfa"/>
    <stop offset="100%" stop-color="#6366f1"/>
  </radialGradient>

  <!-- Off-centre highlight (light from top-left) -->
  <radialGradient id="grad-highlight" cx="35%" cy="35%" r="65%">
    <stop offset="0%" stop-color="#ffffff" stop-opacity="0.4"/>
    <stop offset="100%" stop-color="#ffffff" stop-opacity="0"/>
  </radialGradient>
</defs>

<circle cx="12" cy="12" r="10" fill="url(#grad-radial)"/>
<!-- Overlay highlight on top -->
<circle cx="12" cy="12" r="10" fill="url(#grad-highlight)"/>
```

### Gradient with Transparency
Fade a shape to transparent — useful for soft shadows or background washes.
```svg
<defs>
  <linearGradient id="grad-fade" x1="0" y1="0" x2="0" y2="1">
    <stop offset="0%" stop-color="#6366f1" stop-opacity="1"/>
    <stop offset="100%" stop-color="#6366f1" stop-opacity="0"/>
  </linearGradient>
</defs>

<rect x="2" y="2" width="20" height="20" rx="5" fill="url(#grad-fade)"/>
```

### Gradient on a Stroke
Gradients can also be applied to strokes, not just fills.
```svg
<defs>
  <linearGradient id="grad-stroke" x1="0" y1="0" x2="1" y2="0">
    <stop offset="0%" stop-color="#06b6d4"/>
    <stop offset="100%" stop-color="#6366f1"/>
  </linearGradient>
</defs>

<circle cx="12" cy="12" r="10"
  fill="none"
  stroke="url(#grad-stroke)"
  stroke-width="2"/>
```

### Gradient Recipes for Common Combinations

| Name | Colors | Direction | Best used on |
|---|---|---|---|
| Ocean | `#06b6d4` → `#3b82f6` | left → right | circles, hexagons |
| Sunset | `#f59e0b` → `#ef4444` | top → bottom | shields, diamonds |
| Aurora | `#6366f1` → `#8b5cf6` | diagonal | rounded rects |
| Mint | `#10b981` → `#06b6d4` | top → bottom | rounded rects |
| Rose | `#f43f5e` → `#f97316` | diagonal | circles, hearts |
| Slate | `#475569` → `#1e293b` | top → bottom | any — neutral/dark UI |
| Soft highlight | `rgba(255,255,255,0.4)` → transparent | top-left radial | overlay on any filled shape |

### Tips

- Always define gradients in `<defs>` — never inline them on elements.
- Use `gradientUnits="objectBoundingBox"` (the default) so coordinates are
  relative (0–1) and the gradient scales with the shape automatically.
- Switch to `gradientUnits="userSpaceOnUse"` only when you need the gradient
  to span multiple separate shapes with one consistent direction.
- Avoid more than 3 colour stops in an icon — it becomes noisy at small sizes.
- For a "glass" effect: fill shape with a solid colour, then overlay a radial
  gradient from `white` at 30% opacity to transparent.

---

## Pixel-Hinting for Small Sizes

For icons rendered at 16px or below, shift coordinates to sit on 0.5-pixel
boundaries to avoid blurry rendering on non-retina screens:

```svg
<!-- Instead of: -->
<line x1="4" y1="6" x2="20" y2="6"/>
<!-- Use: -->
<line x1="4.5" y1="6.5" x2="19.5" y2="6.5"/>
```

---

## Animation Snippets

### Spinner (CSS)
```svg
<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
  <circle cx="12" cy="12" r="10" stroke-opacity="0.25"/>
  <path d="M12 2a10 10 0 0 1 10 10" stroke-linecap="round">
    <animateTransform attributeName="transform" type="rotate"
      from="0 12 12" to="360 12 12" dur="0.8s" repeatCount="indefinite"/>
  </path>
</svg>
```

### Pulse dot
```svg
<circle cx="12" cy="12" r="4" fill="currentColor">
  <animate attributeName="r" values="4;8;4" dur="1.5s" repeatCount="indefinite"/>
  <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite"/>
</circle>
```

---

## Output Checklist

Before returning an icon, verify:

- [ ] `viewBox` is square and appropriate for the icon's detail level
- [ ] No `width` or `height` attributes on `<svg>`
- [ ] `role="img"` and `<title>` present
- [ ] Uses `currentColor` (not hardcoded hex values) unless two-color style
- [ ] Paths are clean — no unnecessary precision (round to 2 decimal places)
- [ ] Visually balanced within the viewBox with ~1–2px padding from edges
- [ ] Tested mentally at 16px, 24px, and 48px sizes

---

## Example Workflow

**User:** "Give me an SVG icon for a notification bell"

1. Identify style: outline (default for UI icons)
2. Sketch geometry: bell body (arc + straight sides), clapper (small circle), hanger (small arc at top)
3. Choose viewBox: `0 0 24 24`
4. Build paths using primitives
5. Run checklist
6. Return clean SVG with brief explanation of the geometry used

---

## Related Topics

- Heroicons, Lucide, Phosphor, Tabler — reference icon sets for style consistency
- SVGO — tool for optimizing SVG output before shipping to production
- `<symbol>` + `<use>` — sprite pattern for using multiple icons efficiently
- CSS `mask-image` — technique for using SVG icons as CSS masks

---

## Icon Studio Tool

When the user asks to **open**, **launch**, or **use** the SVG Icon Studio (or asks
for a GUI / visual tool to generate and manage icons), create or serve the
following self-contained HTML file. It provides:

- AI-powered icon generation via the Anthropic API
- Style, size, background shape, and gradient controls
- Live preview at multiple sizes
- Persistent library saved to `localStorage`
- SVG + PNG download, library export/import as JSON

Save it as `svg-icon-studio.html` and open it in the browser, or return it
directly as an artifact.

### Triggers
- "open the icon studio"
- "launch the icon tool"
- "show me the icon manager"
- "I want a GUI for generating icons"

### File: `svg-icon-studio.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>SVG Icon Studio</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Syne:wght@400;600;700;800&display=swap');
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  :root {
    --bg: #0a0a0f; --surface: #13131a; --surface2: #1c1c27; --border: #2a2a3a;
    --accent: #7c6aff; --accent2: #00d4aa; --accent3: #ff6b6b;
    --text: #e8e8f0; --text2: #888899;
    --mono: 'DM Mono', monospace; --sans: 'Syne', sans-serif;
  }
  body { font-family: var(--sans); background: var(--bg); color: var(--text); min-height: 100vh; display: grid; grid-template-rows: auto 1fr; overflow: hidden; }
  header { padding: 16px 24px; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 12px; background: var(--surface); }
  header h1 { font-size: 18px; font-weight: 800; letter-spacing: -0.5px; background: linear-gradient(135deg, var(--accent), var(--accent2)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
  header .badge { font-family: var(--mono); font-size: 10px; padding: 2px 8px; border-radius: 4px; background: rgba(124,106,255,0.15); color: var(--accent); border: 1px solid rgba(124,106,255,0.3); }
  .layout { display: grid; grid-template-columns: 340px 1fr 280px; height: calc(100vh - 57px); overflow: hidden; }
  .left-panel { border-right: 1px solid var(--border); display: flex; flex-direction: column; background: var(--surface); }
  .panel-title { font-size: 10px; font-weight: 700; letter-spacing: 1.5px; text-transform: uppercase; color: var(--text2); padding: 14px 16px 10px; border-bottom: 1px solid var(--border); }
  .prompt-area { padding: 14px; display: flex; flex-direction: column; gap: 10px; border-bottom: 1px solid var(--border); }
  textarea { font-family: var(--mono); font-size: 12px; background: var(--surface2); border: 1px solid var(--border); border-radius: 8px; color: var(--text); padding: 10px 12px; resize: none; height: 80px; outline: none; transition: border-color 0.2s; line-height: 1.6; }
  textarea:focus { border-color: var(--accent); }
  textarea::placeholder { color: var(--text2); }
  .options-row { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  select { font-family: var(--mono); font-size: 11px; background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; color: var(--text); padding: 7px 10px; outline: none; cursor: pointer; transition: border-color 0.2s; }
  select:focus { border-color: var(--accent); }
  .gen-btn { font-family: var(--sans); font-size: 13px; font-weight: 700; background: linear-gradient(135deg, var(--accent), #5b4de8); color: #fff; border: none; border-radius: 8px; padding: 10px; cursor: pointer; transition: opacity 0.2s, transform 0.1s; display: flex; align-items: center; justify-content: center; gap: 8px; }
  .gen-btn:hover { opacity: 0.9; } .gen-btn:active { transform: scale(0.98); } .gen-btn:disabled { opacity: 0.5; cursor: not-allowed; }
  .gen-btn .spinner { width: 14px; height: 14px; border: 2px solid rgba(255,255,255,0.3); border-top-color: #fff; border-radius: 50%; animation: spin 0.7s linear infinite; display: none; }
  .gen-btn.loading .spinner { display: block; } .gen-btn.loading .btn-label { display: none; }
  @keyframes spin { to { transform: rotate(360deg); } }
  .library-scroll { flex: 1; overflow-y: auto; padding: 12px; display: flex; flex-direction: column; gap: 8px; }
  .library-scroll::-webkit-scrollbar { width: 4px; } .library-scroll::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }
  .icon-card { background: var(--surface2); border: 1px solid var(--border); border-radius: 10px; padding: 10px 12px; display: flex; align-items: center; gap: 12px; cursor: pointer; transition: border-color 0.2s, background 0.2s; }
  .icon-card:hover { border-color: var(--accent); background: rgba(124,106,255,0.05); }
  .icon-card.active { border-color: var(--accent); background: rgba(124,106,255,0.1); }
  .icon-thumb { width: 40px; height: 40px; border-radius: 8px; background: var(--surface); display: flex; align-items: center; justify-content: center; flex-shrink: 0; overflow: hidden; }
  .icon-meta { flex: 1; min-width: 0; }
  .icon-name { font-size: 12px; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; margin-bottom: 2px; }
  .icon-style-tag { font-family: var(--mono); font-size: 9px; color: var(--text2); text-transform: uppercase; letter-spacing: 0.5px; }
  .icon-actions { display: flex; gap: 4px; }
  .icon-action-btn { width: 26px; height: 26px; border-radius: 6px; background: transparent; border: 1px solid var(--border); color: var(--text2); cursor: pointer; display: flex; align-items: center; justify-content: center; transition: all 0.15s; font-size: 11px; }
  .icon-action-btn:hover { border-color: var(--accent3); color: var(--accent3); }
  .icon-action-btn.download:hover { border-color: var(--accent2); color: var(--accent2); }
  .empty-library { display: flex; flex-direction: column; align-items: center; justify-content: center; height: 160px; gap: 8px; color: var(--text2); font-size: 12px; text-align: center; }
  .empty-library svg { opacity: 0.3; }
  .center-panel { display: flex; flex-direction: column; background: var(--bg); }
  .preview-area { flex: 1; display: flex; align-items: center; justify-content: center; position: relative; overflow: hidden; }
  .preview-bg { position: absolute; inset: 0; background-image: radial-gradient(circle at 30% 40%, rgba(124,106,255,0.06) 0%, transparent 60%), radial-gradient(circle at 70% 70%, rgba(0,212,170,0.04) 0%, transparent 50%); }
  .preview-checkerboard { position: absolute; inset: 0; background-image: linear-gradient(45deg, rgba(255,255,255,0.02) 25%, transparent 25%), linear-gradient(-45deg, rgba(255,255,255,0.02) 25%, transparent 25%), linear-gradient(45deg, transparent 75%, rgba(255,255,255,0.02) 75%), linear-gradient(-45deg, transparent 75%, rgba(255,255,255,0.02) 75%); background-size: 20px 20px; background-position: 0 0, 0 10px, 10px -10px, -10px 0px; }
  .preview-icon { position: relative; z-index: 1; transition: all 0.3s; }
  .preview-icon svg { filter: drop-shadow(0 0 40px rgba(124,106,255,0.2)); display: block; }
  .preview-placeholder { position: relative; z-index: 1; display: flex; flex-direction: column; align-items: center; gap: 12px; color: var(--text2); text-align: center; }
  .preview-placeholder svg { opacity: 0.2; } .preview-placeholder p { font-size: 13px; }
  .size-controls { position: absolute; bottom: 20px; left: 50%; transform: translateX(-50%); display: flex; gap: 6px; z-index: 2; }
  .size-btn { font-family: var(--mono); font-size: 10px; padding: 4px 10px; border-radius: 4px; background: var(--surface); border: 1px solid var(--border); color: var(--text2); cursor: pointer; transition: all 0.15s; }
  .size-btn:hover, .size-btn.active { border-color: var(--accent); color: var(--accent); background: rgba(124,106,255,0.1); }
  .code-panel { border-top: 1px solid var(--border); background: var(--surface); max-height: 200px; display: flex; flex-direction: column; }
  .code-header { display: flex; align-items: center; justify-content: space-between; padding: 8px 14px; border-bottom: 1px solid var(--border); }
  .code-header span { font-family: var(--mono); font-size: 10px; color: var(--text2); text-transform: uppercase; letter-spacing: 1px; }
  .copy-btn { font-family: var(--mono); font-size: 10px; padding: 3px 10px; border-radius: 4px; background: transparent; border: 1px solid var(--border); color: var(--text2); cursor: pointer; transition: all 0.15s; }
  .copy-btn:hover, .copy-btn.copied { border-color: var(--accent2); color: var(--accent2); }
  .code-scroll { flex: 1; overflow: auto; padding: 12px 14px; }
  .code-scroll::-webkit-scrollbar { height: 4px; width: 4px; } .code-scroll::-webkit-scrollbar-thumb { background: var(--border); }
  pre { font-family: var(--mono); font-size: 11px; line-height: 1.7; color: var(--text2); white-space: pre; }
  .right-panel { border-left: 1px solid var(--border); background: var(--surface); display: flex; flex-direction: column; overflow-y: auto; }
  .right-panel::-webkit-scrollbar { width: 4px; } .right-panel::-webkit-scrollbar-thumb { background: var(--border); }
  .props-section { padding: 14px; border-bottom: 1px solid var(--border); }
  .props-section-title { font-size: 10px; font-weight: 700; letter-spacing: 1.2px; text-transform: uppercase; color: var(--text2); margin-bottom: 12px; }
  .prop-row { display: flex; align-items: center; justify-content: space-between; margin-bottom: 10px; gap: 10px; }
  .prop-label { font-family: var(--mono); font-size: 11px; color: var(--text2); flex-shrink: 0; }
  .color-swatch { width: 20px; height: 20px; border-radius: 4px; border: 1px solid var(--border); cursor: pointer; flex-shrink: 0; }
  input[type="color"] { width: 0; height: 0; opacity: 0; position: absolute; }
  .color-row { display: flex; align-items: center; gap: 8px; }
  .color-hex { font-family: var(--mono); font-size: 11px; background: var(--surface2); border: 1px solid var(--border); border-radius: 4px; color: var(--text); padding: 4px 8px; width: 80px; outline: none; }
  .size-input { font-family: var(--mono); font-size: 11px; background: var(--surface2); border: 1px solid var(--border); border-radius: 4px; color: var(--text); padding: 4px 8px; width: 60px; outline: none; text-align: right; }
  .action-btns { display: flex; flex-direction: column; gap: 8px; padding: 14px; }
  .action-btn { font-family: var(--sans); font-size: 12px; font-weight: 600; padding: 9px 14px; border-radius: 8px; border: 1px solid var(--border); cursor: pointer; display: flex; align-items: center; gap: 8px; transition: all 0.15s; background: var(--surface2); color: var(--text); }
  .action-btn:hover { border-color: var(--accent); color: var(--accent); background: rgba(124,106,255,0.08); }
  .action-btn.save { border-color: rgba(0,212,170,0.3); color: var(--accent2); background: rgba(0,212,170,0.05); }
  .action-btn.save:hover { border-color: var(--accent2); background: rgba(0,212,170,0.1); }
  .action-btn.download { border-color: rgba(124,106,255,0.3); color: var(--accent); background: rgba(124,106,255,0.05); }
  .action-btn:disabled { opacity: 0.4; cursor: not-allowed; }
  .error-msg { font-family: var(--mono); font-size: 10px; color: var(--accent3); padding: 8px 14px; background: rgba(255,107,107,0.08); border: 1px solid rgba(255,107,107,0.2); border-radius: 6px; margin: 0 14px 10px; display: none; }
  .toast { position: fixed; bottom: 24px; right: 24px; background: var(--surface2); border: 1px solid var(--accent2); color: var(--accent2); font-family: var(--mono); font-size: 12px; padding: 10px 16px; border-radius: 8px; z-index: 100; opacity: 0; transform: translateY(8px); transition: all 0.2s; pointer-events: none; }
  .toast.show { opacity: 1; transform: translateY(0); }
  .name-input { font-family: var(--mono); font-size: 11px; background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; color: var(--text); padding: 6px 10px; outline: none; width: 100%; transition: border-color 0.2s; }
  .name-input:focus { border-color: var(--accent); }
  .bg-options { display: flex; gap: 6px; flex-wrap: wrap; }
  .bg-opt { width: 24px; height: 24px; border-radius: 5px; cursor: pointer; border: 2px solid transparent; transition: border-color 0.15s; }
  .bg-opt.active { border-color: var(--accent); }
</style>
</head>
<body>
<header>
  <h1>SVG Icon Studio</h1>
  <span class="badge">AI Powered</span>
</header>
<div class="layout">
  <div class="left-panel">
    <div class="panel-title">Generate</div>
    <div class="prompt-area">
      <textarea id="prompt" placeholder="Describe your icon… e.g. a lightning bolt inside a rounded square with a teal gradient"></textarea>
      <div class="options-row">
        <select id="style"><option value="outline">Outline</option><option value="solid">Solid / Filled</option><option value="duotone">Duotone</option><option value="two-color">Two-Color</option></select>
        <select id="size"><option value="24">24 × 24</option><option value="32">32 × 32</option><option value="48">48 × 48</option><option value="64">64 × 64</option></select>
      </div>
      <div class="options-row">
        <select id="background"><option value="none">No background</option><option value="circle">Circle BG</option><option value="rounded-rect">Rounded Rect BG</option><option value="shield">Shield BG</option><option value="hexagon">Hexagon BG</option></select>
        <select id="gradient"><option value="none">No gradient</option><option value="ocean">Ocean</option><option value="sunset">Sunset</option><option value="aurora">Aurora</option><option value="mint">Mint</option><option value="rose">Rose</option><option value="slate">Slate</option></select>
      </div>
      <button class="gen-btn" id="genBtn" onclick="generateIcon()">
        <div class="spinner"></div><span class="btn-label">✦ Generate Icon</span>
      </button>
    </div>
    <div class="panel-title" style="margin-top:0">Library (<span id="libCount">0</span>)</div>
    <div class="library-scroll" id="library">
      <div class="empty-library">
        <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="3"/><path d="M12 8v8M8 12h8"/></svg>
        <p>Generated icons will<br>appear here</p>
      </div>
    </div>
  </div>
  <div class="center-panel">
    <div class="preview-area" id="previewArea">
      <div class="preview-bg"></div>
      <div class="preview-checkerboard"></div>
      <div class="preview-placeholder" id="placeholder">
        <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1"><circle cx="12" cy="12" r="10"/><path d="M12 8v4l3 3"/></svg>
        <p>Generate or select an icon<br>to preview it here</p>
      </div>
      <div class="preview-icon" id="previewIcon" style="display:none"></div>
      <div class="size-controls" id="sizeControls" style="display:none">
        <button class="size-btn" onclick="setPreviewSize(16)">16px</button>
        <button class="size-btn active" onclick="setPreviewSize(80)">80px</button>
        <button class="size-btn" onclick="setPreviewSize(160)">160px</button>
        <button class="size-btn" onclick="setPreviewSize(320)">320px</button>
      </div>
    </div>
    <div class="code-panel">
      <div class="code-header">
        <span>SVG Source</span>
        <button class="copy-btn" id="copyBtn" onclick="copyCode()">Copy</button>
      </div>
      <div class="code-scroll"><pre id="codeOutput"><span style="color:var(--border)">// SVG code will appear here</span></pre></div>
    </div>
  </div>
  <div class="right-panel">
    <div class="panel-title">Properties</div>
    <div class="props-section">
      <div class="props-section-title">Name</div>
      <input type="text" class="name-input" id="iconName" placeholder="icon-name" value=""/>
    </div>
    <div class="props-section">
      <div class="props-section-title">Color</div>
      <div class="color-row">
        <div class="color-swatch" id="colorSwatch" style="background:#7c6aff" onclick="document.getElementById('colorPicker').click()"></div>
        <input type="color" id="colorPicker" value="#7c6aff" oninput="updateColor(this.value)"/>
        <input type="text" class="color-hex" id="colorHex" value="#7c6aff" oninput="updateColorFromHex(this.value)"/>
        <button class="icon-action-btn" onclick="applyColor()" style="width:auto;padding:0 8px;font-size:10px;font-family:var(--mono)">Apply</button>
      </div>
    </div>
    <div class="props-section">
      <div class="props-section-title">Preview Background</div>
      <div class="bg-options">
        <div class="bg-opt active" style="background:#0a0a0f" onclick="setPreviewBg('#0a0a0f',this)" title="Dark"></div>
        <div class="bg-opt" style="background:#ffffff" onclick="setPreviewBg('#ffffff',this)" title="White"></div>
        <div class="bg-opt" style="background:#f0f0f5" onclick="setPreviewBg('#f0f0f5',this)" title="Light"></div>
        <div class="bg-opt" style="background:#1a1a2e" onclick="setPreviewBg('#1a1a2e',this)" title="Navy"></div>
        <div class="bg-opt" style="background:linear-gradient(135deg,#667eea,#764ba2)" onclick="setPreviewBg('linear-gradient(135deg,#667eea,#764ba2)',this)" title="Purple"></div>
        <div class="bg-opt" style="background:linear-gradient(135deg,#f093fb,#f5576c)" onclick="setPreviewBg('linear-gradient(135deg,#f093fb,#f5576c)',this)" title="Pink"></div>
      </div>
    </div>
    <div class="props-section">
      <div class="props-section-title">Export Size</div>
      <div class="prop-row">
        <span class="prop-label">Width (px)</span>
        <input type="number" class="size-input" id="exportSize" value="512" min="16" max="2048"/>
      </div>
    </div>
    <div class="error-msg" id="errorMsg"></div>
    <div class="action-btns">
      <button class="action-btn save" id="saveBtn" onclick="saveIcon()" disabled>
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg>
        Save to Library
      </button>
      <button class="action-btn download" id="downloadSvgBtn" onclick="downloadSVG()" disabled>
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        Download SVG
      </button>
      <button class="action-btn" id="downloadPngBtn" onclick="downloadPNG()" disabled>
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>
        Download PNG
      </button>
      <button class="action-btn" onclick="exportLibrary()">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
        Export Library JSON
      </button>
      <button class="action-btn" onclick="document.getElementById('importFile').click()">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>
        Import Library JSON
      </button>
      <input type="file" id="importFile" accept=".json" style="display:none" onchange="importLibrary(event)"/>
    </div>
  </div>
</div>
<div class="toast" id="toast"></div>
<script>
let currentSVG = null;
let library = JSON.parse(localStorage.getItem('svg-icon-library') || '[]');
let previewSize = 80;
const GRADIENTS = { ocean:['#06b6d4','#3b82f6'], sunset:['#f59e0b','#ef4444'], aurora:['#6366f1','#8b5cf6'], mint:['#10b981','#06b6d4'], rose:['#f43f5e','#f97316'], slate:['#475569','#1e293b'] };
renderLibrary();

async function generateIcon() {
  const prompt = document.getElementById('prompt').value.trim();
  if (!prompt) { showError('Please describe your icon first.'); return; }
  const style = document.getElementById('style').value;
  const size = document.getElementById('size').value;
  const bg = document.getElementById('background').value;
  const grad = document.getElementById('gradient').value;
  const btn = document.getElementById('genBtn');
  btn.disabled = true; btn.classList.add('loading'); hideError();
  const systemPrompt = `You are an expert SVG icon designer. Output ONLY the raw SVG element — no markdown fences, no explanation, no backticks.\nRules:\n- viewBox="0 0 ${size} ${size}"\n- No width or height on <svg>\n- xmlns="http://www.w3.org/2000/svg"\n- role="img" and <title>\n- Use currentColor unless gradient requested\n- Round coords to 2 decimal places\n- Padding ~${Math.round(size*0.08)}px from edges\n- Style: ${style}\n${bg!=='none'?`- ${bg} background shape as first element`:''}\n${grad!=='none'?`- ${grad} gradient (${GRADIENTS[grad]?.join(' → ')}) via <defs><linearGradient>`:''}\nOutput ONLY the SVG element.`;
  const userPrompt = `Create a ${style} SVG icon: "${prompt}"${bg!=='none'?` with ${bg} background`:''}${grad!=='none'?` using ${grad} gradient`:''}`;
  try {
    const res = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'anthropic-dangerous-direct-browser-access': 'true' },
      body: JSON.stringify({ model: 'claude-sonnet-4-20250514', max_tokens: 1000, system: systemPrompt, messages: [{ role: 'user', content: userPrompt }] })
    });
    const data = await res.json();
    if (data.error) throw new Error(data.error.message);
    const raw = data.content.map(b => b.text||'').join('').trim();
    const cleaned = raw.replace(/```[a-z]*\n?/gi,'').trim();
    const start = cleaned.indexOf('<svg');
    const end = cleaned.lastIndexOf('</svg>');
    if (start===-1||end===-1) throw new Error('No valid SVG in response. Try again.');
    const svg = cleaned.slice(start, end+6);
    currentSVG = svg;
    const name = prompt.toLowerCase().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'').slice(0,30);
    document.getElementById('iconName').value = name;
    showPreview(svg); showCode(svg); enableActions();
  } catch(e) { showError('Generation failed: ' + e.message); }
  btn.disabled = false; btn.classList.remove('loading');
}

function showPreview(svg) {
  const el = document.getElementById('previewIcon');
  el.innerHTML = svg;
  const s = el.querySelector('svg');
  if (s) { s.style.width = previewSize+'px'; s.style.height = previewSize+'px'; }
  el.style.display = 'block';
  document.getElementById('placeholder').style.display = 'none';
  document.getElementById('sizeControls').style.display = 'flex';
}

function showCode(svg) {
  document.getElementById('codeOutput').textContent =
    svg.replace(/></g,'>\n  <').replace(/  <\//g,'</').replace(/>\n  <\/svg>/g,'>\n</svg>');
}

function setPreviewSize(px) {
  previewSize = px;
  document.querySelectorAll('.size-btn').forEach(b=>b.classList.remove('active'));
  event.target.classList.add('active');
  if (currentSVG) showPreview(currentSVG);
}

function setPreviewBg(bg, el) {
  document.querySelectorAll('.bg-opt').forEach(b=>b.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('previewArea').style.background = bg;
}

function updateColor(val) { document.getElementById('colorSwatch').style.background=val; document.getElementById('colorHex').value=val; }
function updateColorFromHex(val) { if(/^#[0-9a-fA-F]{6}$/.test(val)) { document.getElementById('colorPicker').value=val; document.getElementById('colorSwatch').style.background=val; } }
function applyColor() {
  if (!currentSVG) return;
  const c = document.getElementById('colorHex').value;
  showPreview(currentSVG.replace(/currentColor/g,c).replace(/stroke="[^"]*"/g,m=>m.includes('none')?m:`stroke="${c}"`).replace(/fill="[^"]*"/g,m=>m.includes('none')||m.includes('url')?m:`fill="${c}"`));
}

function enableActions() { ['saveBtn','downloadSvgBtn','downloadPngBtn'].forEach(id=>document.getElementById(id).disabled=false); }

function saveIcon() {
  if (!currentSVG) return;
  const name = document.getElementById('iconName').value||'icon-'+Date.now();
  library.unshift({ id:Date.now(), name, style:document.getElementById('style').value, svg:currentSVG });
  localStorage.setItem('svg-icon-library', JSON.stringify(library));
  renderLibrary(); showToast('Saved to library ✓');
}

function renderLibrary() {
  const el = document.getElementById('library');
  document.getElementById('libCount').textContent = library.length;
  if (library.length===0) { el.innerHTML=`<div class="empty-library"><svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="3" y="3" width="18" height="18" rx="3"/><path d="M12 8v8M8 12h8"/></svg><p>Generated icons will<br>appear here</p></div>`; return; }
  el.innerHTML = library.map((icon,i)=>`<div class="icon-card" id="card-${icon.id}" onclick="selectIcon(${i})"><div class="icon-thumb" style="color:#a0a0c0">${icon.svg}</div><div class="icon-meta"><div class="icon-name">${icon.name}</div><div class="icon-style-tag">${icon.style}</div></div><div class="icon-actions"><button class="icon-action-btn download" onclick="event.stopPropagation();downloadIconSVG(${i})" title="Download">↓</button><button class="icon-action-btn" onclick="event.stopPropagation();deleteIcon(${i})" title="Delete">×</button></div></div>`).join('');
  el.querySelectorAll('.icon-thumb svg').forEach(s=>{ s.removeAttribute('width'); s.removeAttribute('height'); s.style.cssText='width:28px;height:28px;display:block;overflow:visible'; });
}

function selectIcon(i) {
  const icon = library[i]; currentSVG = icon.svg;
  document.getElementById('iconName').value = icon.name;
  showPreview(icon.svg); showCode(icon.svg); enableActions();
  document.querySelectorAll('.icon-card').forEach(c=>c.classList.remove('active'));
  document.getElementById('card-'+icon.id)?.classList.add('active');
}

function deleteIcon(i) { library.splice(i,1); localStorage.setItem('svg-icon-library',JSON.stringify(library)); renderLibrary(); showToast('Deleted'); }

function downloadSVG() {
  if (!currentSVG) return;
  const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([currentSVG],{type:'image/svg+xml'})); a.download=(document.getElementById('iconName').value||'icon')+'.svg'; a.click();
}

function downloadIconSVG(i) {
  const icon=library[i]; const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([icon.svg],{type:'image/svg+xml'})); a.download=icon.name+'.svg'; a.click();
}

function downloadPNG() {
  if (!currentSVG) return;
  const size=parseInt(document.getElementById('exportSize').value)||512;
  const name=document.getElementById('iconName').value||'icon';
  const canvas=document.createElement('canvas'); canvas.width=canvas.height=size;
  const img=new Image();
  const blob=new Blob([currentSVG.replace('<svg',`<svg width="${size}" height="${size}"`)],{type:'image/svg+xml'});
  const url=URL.createObjectURL(blob);
  img.onload=()=>{ canvas.getContext('2d').drawImage(img,0,0,size,size); URL.revokeObjectURL(url); const a=document.createElement('a'); a.href=canvas.toDataURL('image/png'); a.download=name+'.png'; a.click(); };
  img.src=url;
}

function exportLibrary() {
  const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([JSON.stringify(library,null,2)],{type:'application/json'})); a.download='icon-library.json'; a.click(); showToast('Library exported ✓');
}

function importLibrary(e) {
  const file=e.target.files[0]; if(!file) return;
  const r=new FileReader(); r.onload=ev=>{ try { const d=JSON.parse(ev.target.result); if(Array.isArray(d)){ library=[...d,...library]; localStorage.setItem('svg-icon-library',JSON.stringify(library)); renderLibrary(); showToast(`Imported ${d.length} icons ✓`); } } catch { showError('Invalid JSON file'); } }; r.readAsText(file); e.target.value='';
}

function copyCode() {
  const code=document.getElementById('codeOutput').textContent;
  if(code.startsWith('//')) return;
  navigator.clipboard.writeText(code).then(()=>{ const b=document.getElementById('copyBtn'); b.textContent='Copied!'; b.classList.add('copied'); setTimeout(()=>{ b.textContent='Copy'; b.classList.remove('copied'); },1500); });
}

function showError(msg) { const e=document.getElementById('errorMsg'); e.textContent=msg; e.style.display='block'; }
function hideError() { document.getElementById('errorMsg').style.display='none'; }
function showToast(msg) { const t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),2000); }

document.getElementById('prompt').addEventListener('keydown', e=>{ if(e.key==='Enter'&&(e.metaKey||e.ctrlKey)) generateIcon(); });
</script>
</body>
</html>
```
