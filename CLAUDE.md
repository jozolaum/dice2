# CLAUDE.md — Dado Arcano (dice2)

## Always Do First
- **Read the `frontend-design` skill** before writing any frontend code, every session, no exceptions.
- Check the `assets/` folder for SVG dice files and reference images before designing anything.

## Project Context
**Dado Arcano** is a mobile-first RPG dice roller web app (single `index.html`).  
The visual direction is **D&D 1980s rulebook** — think aged parchment, woodcut engravings, 
heavy serif typography, ink textures, and the tactile feel of a physical game manual.  
This is NOT a dark/neon aesthetic. It is warm, analog, and nostalgic.

## Functional Features (DO NOT BREAK)
The app has these working features — redesign visual only, never remove or break logic:
- **Dice bar** (fixed bottom, 2 rows): D4, D6, D8, D10, D12, D20, D100
- **Dice queue**: tap dice to add to queue, chips with × to remove individually
- **Bonus system**: appears after first die selected, − 0 + control, range -10 to +20
  - Shows as chip in queue when ≠ 0
  - Shows as result card alongside dice cards
  - Persists until "Nova Rolagem" is clicked
- **Slot machine animation**: numbers cycle fast → slow → lock, staggered 300ms per die
- **Critical hit**: max value → gold color + "✦ CRÍTICO" label
- **Critical fail**: value 1 → red color + "FALHA" label  
- **All-max bonus**: full-screen gold flash
- **Roll history**: last 5 rolls, most recent first, format "2× D20 + bônus +3 → 15,4 = 22"
- **Rerolar button**: rerols same combo with same bonus
- **Nova Rolagem button**: clears queue, results, bonus (keeps history)

## Assets
- `assets/dice/` — SVG files for all 7 dice. Use these exactly as provided.
- `assets/ref/` — Reference images for visual style (D&D artwork, typography, textures).
  Study these before designing. Extract: color palette, texture style, typography feel.

## Visual Direction — D&D 1980s Rulebook

### Mood
Aged paper, ink on parchment, woodcut illustrations, candlelight warmth.  
Feels like you found a weathered rulebook at a yard sale.  
NOT dark/moody. NOT neon. NOT minimal. Warm, textured, characterful.

### Color Palette (derive everything from these)
- Background: warm parchment — `#f4e8c1` or `#ede0b0` (aged paper)
- Primary ink: near-black with warm tone — `#1a1209`
- Accent red: deep crimson — `#8b1a1a` (classic D&D red)
- Accent gold: aged brass — `#b8860b`
- Secondary: dark brown — `#3d1f0a`
- Muted text: `#6b4c2a`
- Critical gold: `#c8960c`
- Fail red: `#8b1a1a`

### Typography
- **Display/headings**: MedievalSharp, MedievalSharp, Cinzel Decorative, or IM Fell English — 
  pick one that screams "fantasy rulebook". Load from Google Fonts.
- **Body/labels**: Crimson Text or EB Garamond — warm, readable, period-appropriate serif.
- **Numbers/results**: The display font, large, dramatic.
- **Monospace elements** (history log): Special Elite or Courier Prime.
- Apply tight tracking on headings. Never use sans-serif anywhere.

### Texture & Depth
- Background: parchment texture via CSS (layered radial gradients in warm tones 
  + SVG noise filter for grain). Should feel like aged paper, not flat color.
- Cards/surfaces: slightly darker parchment with subtle inner shadow, 
  like paper lifted off the page.
- Borders: thin, slightly irregular lines in dark brown/crimson. 
  Consider ornamental corners on major containers.
- Decorative elements: use ❧ ✦ ◆ — ∙ as separators and accents.
- The dice bar at the bottom: darker, like a leather or wood surface.

### Shadows & Depth System
- Base layer: parchment background
- Elevated (cards, chips): warm sepia shadow `rgba(61,31,10,0.25)`
- Floating (buttons, active elements): deeper shadow + slight lift
- Never use cool-toned or black shadows — always warm brown tones

### Interactive States (every clickable element needs all three)
- Hover: slight lift (translateY -2px), shadow deepens, border darkens
- Active/tap: press down (scale 0.97), shadow collapses
- Focus-visible: crimson outline, 2px offset
- Dice bar buttons: tap pulse scale 0.92 → 1.0, 120ms

### Animations
- Only animate `transform` and `opacity`. Never `transition-all`.
- Spring easing: `cubic-bezier(0.34, 1.56, 0.64, 1)` for entrances
- Ease-out: `cubic-bezier(0.25, 0.46, 0.45, 0.94)` for exits
- Slot machine numbers: keep existing recursive setTimeout logic exactly as-is
- Bonus row entrance: translateY(12px) → 0 + opacity 0 → 1, 280ms spring

### Dice SVGs
- Use files from `assets/dice/` exactly as provided
- Apply `stroke` in dark brown/ink color (`#1a1209` or `#3d1f0a`)
- On hover/selected: stroke shifts to crimson `#8b1a1a`, subtle warm glow
- Size in dice bar: 36×36px. In result cards: larger, more dramatic presence.

## Output Rules
- Single `index.html` file, all CSS inline in `<style>`, all JS inline in `<script>`
- No frameworks, no build steps. Vanilla JS + Google Fonts CDN only.
- Mobile-first, ~390px wide, touch-optimized (min tap target 44px)
- Body does NOT scroll — main content area scrolls internally
- `env(safe-area-inset-bottom)` on dice bar padding
- Accessible: aria-labels on all interactive elements

## Anti-Generic Guardrails
- **Never** use default sans-serif fonts (Inter, Roboto, system-ui)
- **Never** use flat shadows — always warm, layered, color-tinted
- **Never** use `transition-all`
- **Never** use cool blues, purples, or neon as primary colors
- **Never** use a flat solid color as background — always textured parchment
- **Every** surface must belong to the depth layering system
- **Every** clickable element must have hover + active + focus states

## Hard Rules
- Do not remove or break any existing functional feature
- Do not add features not listed above
- Do not use placeholder images — all visual elements are CSS/SVG only
- Do not flatten the design — depth and texture are essential to this aesthetic
