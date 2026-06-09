# Anisha Samanta — UI/UX Portfolio

A design and build brief for a personal portfolio website. The aesthetic borrows the warmth of mid-century print design and pairs it with the restraint of Apple and the editorial confidence of Nike. Vintage in feeling, modern in execution.

> **Implementation status:** This brief reflects the as-built state of `vintage-banner.html`. Sections marked ✅ are fully implemented; remaining sections are aspirational or future work.

---

## 1. Vision & Mood

**One-line concept:** A quiet, confident portfolio that feels like flipping through a beautifully printed monograph — rendered in the browser with subtle motion and glassmorphism.

**Mood references**
- Apple product pages — generous whitespace, anchored typography, deliberate scroll storytelling.
- Nike editorial pages — strong type hierarchy, full-bleed imagery, tactile transitions.
- Vintage Penguin paperbacks, Saul Bass posters, 1960s Swiss & American print, old Polaroids, faded film stock.

**Feel adjectives:** warm, considered, slow, tactile, analog-influenced, modern-minimal, frosted-glass-layer.

---

## 2. Color Palette ✅

A warm, low-saturation vintage palette. Cream-led, never stark white. Inks instead of pure black.

| Role | Name | Hex | Use |
|---|---|---|---|
| Primary background | Paper Cream | `#F5EFE4` | Site background |
| Secondary background | Aged Linen | `#EBE2D2` | Section breaks, cards |
| Primary text / "ink" | Deep Sepia | `#2B221A` | Headings, body |
| Muted text | Faded Ink | `#6E5F4E` | Captions, meta |
| Accent 1 | Burnt Terracotta | `#B6552F` | Links, highlights |
| Accent 2 | Mustard Ochre | `#C9963D` | Tags, callouts |
| Accent 3 | Olive Sage | `#7A8456` | Secondary accent |
| Border / line | Tea-stain | `#D6C8B0` | Hairlines, frames |

**Rules**
- Never use pure white (`#FFFFFF`) or pure black (`#000000`).
- A very subtle paper grain texture overlay (~4% opacity in light, ~2% in dark) is applied globally via `body::before`.
- Horizontal paper-line texture applied via `body::after` at ~2.5% opacity.
- Hover states shift accents by ~10% in luminance, not in hue.

### 2.1 Dark Mode Palette ✅

| Role | Name | Hex | Use |
|---|---|---|---|
| Primary background | Darkroom Ink | `#16100A` | Site background |
| Secondary background | Walnut | `#201810` | Section breaks, cards |
| Primary text | Aged Parchment | `#F0E8D4` | Headings, body |
| Muted text | Faded Brass | `#C0AC90` | Captions, meta |
| Accent 1 | Ember | `#D46C40` | Links, highlights |
| Accent 2 | Amber Glow | `#D4A840` | Tags, callouts |
| Accent 3 | Olive Mist | `#9EAA72` | Secondary accent |
| Border / line | Aged Hairline | `#3A2C1C` | Hairlines, frames |

**Dark-mode rules** — all implemented:
- Deepest color is `#16100A`, a warm near-black (not pure black).
- Paper grain drops to ~2% opacity.
- All colors defined as CSS custom properties on `:root`, overridden under `[data-theme="dark"]`.

### 2.2 Glassmorphism Tokens ✅ (Added)

A frosted-glass layer system sits on top of the vintage palette — warm-tinted transparency rather than cold modern glass.

| Token | Light mode | Dark mode |
|---|---|---|
| `--glass-bg` | `rgba(245,239,228, 0.62)` | `rgba(22,14,6, 0.62)` |
| `--glass-border` | `rgba(201,150,61, 0.20)` | `rgba(212,168,64, 0.16)` |
| `--glass-shine` | `inset 0 1px 0 rgba(255,255,255,0.32)` | `inset 0 1px 0 rgba(255,255,255,0.05)` |
| `--glass-blur` | `blur(14px) saturate(1.5)` | `blur(14px) saturate(1.4)` |

Applied to: nav bar, mobile nav drawer, hero portrait stats, project cards, testimonial cards, credential cards, tabs shell, case-study overlay cards, about-section stats, interest/skill pills, ticket-stub decorative elements.

### 2.3 Theme Implementation ✅

- All colors as CSS custom properties; dark override on `[data-theme="dark"]`.
- Theme toggle stored in `localStorage` under `theme-preference`; falls back to `prefers-color-scheme`.
- Inline `<script>` in `<head>` reads stored preference before stylesheet loads — no flash of wrong theme.
- Theme transitions: `background-color 300ms ease, color 300ms ease` on `body`.

---

## 3. Typography ✅

A two-typeface system loaded from Google Fonts.

**Display / Headings**
- **Cormorant Garamond** (weights 300, 500, 700, italic variants) — `--serif`
- Playfair Display available as fallback

**Body / UI**
- **Inter** — `--body`
- **DM Sans** — `--ui`

**Mono / Accent**
- **DM Mono** — `--mono` — for section labels, tags, ticket serials, credential metadata

**Type scale (desktop)**

| Token | Size | Weight | Usage |
|---|---|---|---|
| Hero name | `clamp(72px, 9vw, 130px)` | 700 | Hero heading |
| Section h2 | `clamp(30px, 3.6vw, 50px)` | 700 italic | Section titles |
| Section label | 10.5px mono, +0.20em | 500 | `01 — WORK` style labels |
| Body large | 18px | 400 italic | Hero tagline, about lead |
| Body | 16px | 400 | Default body |
| Card title | 22px | 900 | Project card titles |
| Caption | 10–11px mono | 400–500 | Tags, ticket metadata |

---

## 4. Layout & Grid ✅

- Max content width 1200px, `0 auto` centered, `28px` side padding.
- Generous vertical section padding: `100–104px` top/bottom.
- 2-column grids on desktop (work cards, about section), single column on mobile.
- `border-radius` system: **all interactive cards use 14–20px rounded corners** (see §2.2).

---

## 5. Iconography & Visual Ephemera ✅ (partially implemented)

The site's visual vocabulary borrows from printed travel and postal ephemera of roughly 1940–1975.

### 5.1 Core Visual Motifs — Implemented

- **Perforated edges** — dashed vertical separator on project cards (`proj-perf-v`) with punch-hole semicircles at card edges.
- **Rubber-stamp marks** — rotated mono labels (`ADMIT ONE`, `VERIFIED`, `SELECTED`) used as ticket stubs and status overlays.
- **Round date-cancellation stamps** — `.postmark` component with city name, wave lines, and portfolio date. Used in Testimonials section header.
- **Ticket serials** — `№ XXXX · PROFESSIONAL` in project card corners via `.proj-ticket-no`.
- **Watermarks** — large faded serif numerals at ~6% opacity behind each section via `::before` pseudo-elements.
- **Wax-seal motif** — circular stamp on hero portrait (`port-stamp`), rotates 15° on hover.
- **Ticker belt** — horizontal scrolling marquee of skills/tools between hero and work sections.

### 5.2 Component Treatments — Implemented

**Project cards (Work section)**
- Ticket-stub format with colored stub, perforated separator, serial number, and category stamp.
- Cards flip 180° on hover to reveal project description and CTA.
- 18px rounded corners + warm glassmorphism background.

**Testimonials carousel**
- Polaroid-style cards in a 3D CSS `perspective` coverflow layout.
- Auto-scrolls; keyboard and dot-nav controls; pauses on hover/focus.
- 20px rounded corners + frosted glass.
- Gold gradient bottom accent bar reveals on active card.
- Postmark decoration in section header.

**Contact section**
- `Say Hello` button links directly to Gmail compose (`mail.google.com/?view=cm&to=...`) — avoids broken `mailto:` behavior.
- Social links as styled mono-label entries in a column.

### 5.3 Certifications Section ✅ (Redesigned — v3)

Replaced folder animation with a professional **3-column credential grid**:
- 6 cards: B.E. Degree, IIIT Bangalore UI/UX, Agentic AI Badge, IxDF Masterclass, Digital Accessibility, Digital Skills Mobile.
- Each card: type tag (mono, gold) + year in header row; italic serif title; issuer + `View ↗` in footer.
- `View ↗` slides in on hover for the 4 cards with certificate PNGs; click opens PNG in new tab.
- Cards reveal with staggered fade-up (80ms per card) via IntersectionObserver + setTimeout.
- After reveal, transition switches to fast `0.24s` hover (lift + shadow + rust left-border).
- Glass background + 16px border-radius.

History:
- v1: Text info-cards with `.cf-card` system.
- v2: Manila folder with 3D peek/fan animation (`.cf-doc`, `cert-folder`).
- v3 (current): Clean credential grid (`.cred-card`, `.cred-grid`).

---

## 6. Navigation ✅

Fixed top bar with backdrop blur and semi-transparent glass background.

```
[ Anisha Samanta ]   [ Work ] [ About ] [ Testimonials ] [ Contact ]   [ ☀ ⇆ ☾ ]
```

- Logo: Cormorant Garamond italic, terracotta underline draws in on hover.
- Links: Inter 13px, 8px rounded hover state, active section gets a gold dot + rust color + rust-tinted background.
- Theme toggle: pill switch with sliding brass thumb, DM Mono labels.
- Nav shrinks on scroll (`padding 24px → 16px`).
- Mobile: collapses to hamburger; slide-in drawer with glass background, `16px` bottom corners.

---

## 7. Section-by-Section ✅

### 7.1 Hero
- Two-column: left = display name + designer title + tagline + CTAs; right = portrait in ornamental frame.
- Parallax: `.hero-glow` at 0.18×, `.vignette` at 0.08×, `.dust` particles at 0.28× scroll speed via `requestAnimationFrame`.
- Scroll cue: vertical gold line + `SCROLL ↓` mono label.
- Portrait: sepia-filtered photo inside ornamental corner-bracket frame with rotatable wax-seal stamp.
- Hero stats card: floating glass panel with `Years Experience`, `Projects`, `Happy Clients`.
- Availability badge with pulsing olive dot.
- Animated dust particles rising in background.

### 7.2 Ticker Belt
- Full-width horizontal marquee of skills: Figma, UX Research, Prototyping, Interaction Design, etc.
- Gradient fade-out on left/right edges.

### 7.3 Design Approach
- 4-column grid (`repeat(4, 1fr)`) with cards for Research, Systems, Motion, Accessibility.
- 16px border-radius grid container; animated top accent bar on hover; springy icon rotation.

### 7.4 Work / Projects ✅
- Glass+tab switcher (Professional / Personal) with sliding ink pill.
- Project cards flip 180° on hover to show description + CTA.
- Ticket-stub aesthetic: colored stub, serial number, perforation line, postmark stamp.
- Scroll reveal: image zooms in from `scale(0.55)` with spring easing.
- Case-study overlay panel slides in for detailed project breakdowns.

### 7.5 About
- Two-column: portrait with ornamental frame + about copy + interest pills.
- Stat strip below portrait (glass + 14px rounded corners).
- Interest/skill pills: 20px pill radius, glass.
- Section linked from nav.

### 7.6 Testimonials
- 3D CSS coverflow carousel: `perspective: 1400px`, cards on virtual arc.
- Auto-scrolls every ~4s; pauses on hover/focus.
- 20px rounded glass cards with gold gradient bottom accent.
- Dot indicators + prev/next arrow buttons.
- Postmark decoration in section heading.

### 7.7 Certifications & Education ✅
See §5.3 above.

### 7.8 Contact / Footer
- Dark ink background section.
- `Let's create something together.` serif heading.
- `Say Hello` button → Gmail compose.
- Social links: LinkedIn, Behance, GitHub, Read.cv — styled as vertical mono-label list.
- Copyright line with current year.

---

## 8. Scroll & Motion System ✅

**Scroll reveal:** IntersectionObserver on `.reveal`, `.reveal-left`, `.reveal-right`, `.reveal-scale` — adds `.in` class at 10% threshold. Stagger via `.d1`–`.d6` transition-delay classes.

**Hero parallax:** `requestAnimationFrame` on scroll — `.hero-glow` at 0.18×, `.vignette` at 0.08×, `.dust` at 0.28×. `will-change: transform` for GPU compositing.

**Credential cards:** custom stagger via setTimeout (80ms/card) + `transitionend` to switch from slow reveal transition to fast hover transition.

**Ticker belt:** CSS `@keyframes ticker` continuous scroll; paused on `prefers-reduced-motion`.

**Testimonial carousel:** JS-driven transform stack; cubic-bezier spring easing `(0.23, 1, 0.32, 1)`.

**Project card flip:** CSS `rotateY(180deg)` with `transform-style: preserve-3d`; 0.7s easing.

**`prefers-reduced-motion`:** Disables parallax, ticker, dust particles, and all transition animations; cards start visible.

---

## 9. Glassmorphism & Rounded Corners System ✅ (Added)

### 9.1 Design Principles

Glassmorphism is applied as a **warm vintage frosted glass** — not cold modern glass. Characteristics:
- Warm amber/cream tinted semi-transparent backgrounds (not white/grey).
- `backdrop-filter: blur(14px) saturate(1.5)` — frosted warmth, not icy clarity.
- Border uses `--gold` color family at low opacity instead of pure `rgba(255,255,255,0.x)`.
- Inner top highlight (`inset 0 1px 0 rgba(255,255,255,0.32)`) simulates light catching the glass edge.

### 9.2 Border Radius Scale

| Component | Radius |
|---|---|
| Nav links | 8px |
| Hamburger button | 10px |
| Mobile nav drawer | 0 0 16px 16px |
| Buttons (primary, ghost, contact, resume) | 10px |
| Social links | 10px |
| Hero stats floating card | 14px |
| Approach grid container | 16px |
| Approach icon box | 12px |
| Tab switcher shell | 14px |
| Tab sliding pill | 10px |
| Project cards (flip faces) | 18px |
| About image frame | 14px |
| About stats strip | 0 0 14px 14px |
| Interest / skill pills | 20px (full pill) |
| Testimonial cards | 20px |
| Testimonial badge | 8px |
| Credential cards | 16px |
| Case study overlay | 20px |
| Case study content cards | 14px |
| Case study icon boxes | 12px |
| Project tags | 8px |
| Ticket stub | 12px |
| Postmark | 8px |
| Focus ring | 6px |

### 9.3 Components with `backdrop-filter`

`backdrop-filter` is effective on elements that float over content with visual depth behind them:
- **Nav** — floats over page content throughout scroll.
- **Mobile nav drawer** — floats over page.
- **Testimonial cards** — float in 3D perspective track.
- **Hero stats card** — floats over portrait gradient.
- **Project cards** — warm glass tint over section background.
- **Credential cards** — subtle glass over certifications section.
- **About stats** — glass below portrait image.
- **Interest pills** — light glass on about section.
- **Case study overlay cards** — float in modal context.
- **Tabs shell** — glass pill container.
- **Ticket stub** — vintage glass decorative element.

---

## 10. Accessibility ✅ (partially implemented)

- Semantic HTML: `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`.
- Skip link: visually hidden until focused; reveals top-left in gold.
- Focus ring: `2px solid var(--gold)`, `3px offset`, `6px border-radius` — visible on keyboard nav.
- All interactive elements keyboard-operable (Enter/Space where applicable).
- `aria-hidden="true"` on decorative elements.
- `prefers-reduced-motion` honored: all animations disabled, cards start visible.
- Testimonial carousel: `role="region"`, `aria-roledescription="carousel"`, dot buttons with `aria-current`.
- Theme toggle: `role="switch"`, `aria-checked`, `aria-label`.
- Work tabs: `role="tablist"`, `aria-selected`, `aria-controls` / `aria-labelledby` pairing.

---

## 11. Tech Stack ✅ (as-built)

| Layer | Choice |
|---|---|
| Framework | Single HTML file (`vintage-banner.html`) — no build step |
| Styling | Vanilla CSS with custom properties; no Tailwind |
| Fonts | Google Fonts (Cormorant Garamond, Inter, DM Mono, DM Sans, Playfair Display) |
| Animation | Vanilla CSS transitions/animations + IntersectionObserver + rAF |
| 3D | CSS `perspective` + `transform-style: preserve-3d` (no WebGL) |
| Glassmorphism | CSS `backdrop-filter` + warm-tinted `rgba` backgrounds |
| Hosting | Static file (local) — deployable to Vercel/Netlify/GitHub Pages |

---

## 12. File Structure

```
Portfolio/
├── vintage-banner.html                         ← entire site (HTML + CSS + JS)
├── anisha-samanta-portfolio-brief.md           ← this document
├── Anisha_Samanta_Resume2026.pdf               ← resume download
├── photo.JPG                                   ← hero portrait
├── Reinvention aith Agentic AI certificate.png ← cert (filename typo preserved)
├── Design system with AI certificate.png       ← cert
├── Digital Accessibility Design certificate.png← cert
└── Digital Skill_Mobile Certificate.png        ← cert
```

---

## 13. Known Notes & Quirks

- **Certificate filename typo:** `Reinvention aith Agentic AI certificate.png` has "aith" instead of "with". This is the actual filename and is referenced exactly as-is in all `src` and `data-cert-img` attributes.
- **`backdrop-filter` browser support:** Requires `-webkit-backdrop-filter` prefix for Safari. Both are included throughout.
- **Project card flip + `filter`:** CSS `filter` breaks `transform-style: preserve-3d`. The glass effect on project cards uses `rgba` background + box-shadow instead of filter.
- **Glass on opaque sections:** `backdrop-filter` is most visible on elements floating over gradients or imagery. On flat section backgrounds, the warm `rgba` tint and `--glass-shine` provide the glass character.

---

*This document reflects the actual as-built state of the portfolio. Last updated: 2026-05-17.*
