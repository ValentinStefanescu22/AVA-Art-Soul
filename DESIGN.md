---
name: AVA Art & Soul
description: autocunoaștere prin creație — clay workshops, counselling and retreats in București
colors:
  ink: "#372B22"
  ink-soft: "#4A3A2E"
  muted: "#6B5D4D"
  sand-50: "#F8F3EB"
  sand-100: "#F2EDE4"
  sand-200: "#E2D6BF"
  sand-300: "#D3C2A4"
  clay-400: "#B8987A"
  clay-500: "#9A7656"
  clay-600: "#765840"
  umber-700: "#5A4230"
  umber-800: "#3E2D21"
  umber-900: "#2A1E16"
  dusk-fg: "#F8F3EB"
  dusk-fg-2: "#E9DCC8"
  dusk-fg-3: "#C9B79C"
  dusk-accent: "#F3D9AE"
  dusk-title: "#FFF4E2"
  dusk-line: "rgba(248,243,235,.16)"
  glow: "#FFE6B8"
  line: "rgba(55,43,34,.16)"
  error: "#8A3B22"
typography:
  display:
    fontFamily: "Pinyon Script, Snell Roundhand, Apple Chancery, cursive"
    fontSize: "clamp(3.2rem, 2rem + 6vw, 7rem)"
    fontWeight: 400
    lineHeight: 0.95
    letterSpacing: "0"
  headline:
    fontFamily: "Fraunces, Iowan Old Style, Palatino Linotype, Georgia, serif"
    fontSize: "clamp(2rem, 1.45rem + 2.4vw, 3.25rem)"
    fontWeight: 350
    lineHeight: 1.08
    letterSpacing: "-0.015em"
  script:
    fontFamily: "Pinyon Script, Snell Roundhand, Apple Chancery, cursive"
    fontSize: "clamp(2.6rem, 1.9rem + 3vw, 4.6rem)"
    fontWeight: 400
    lineHeight: 1.05
    letterSpacing: "0"
  title:
    fontFamily: "Fraunces, Iowan Old Style, Palatino Linotype, Georgia, serif"
    fontSize: "1.7rem"
    fontWeight: 400
    lineHeight: 1.1
  lead:
    fontFamily: "Fraunces, Iowan Old Style, Palatino Linotype, Georgia, serif"
    fontSize: "clamp(1.15rem, 1.05rem + .45vw, 1.4rem)"
    fontWeight: 350
    lineHeight: 1.5
  body:
    fontFamily: "Jost, Avenir Next, Segoe UI, system-ui, sans-serif"
    fontSize: "1.0625rem"
    fontWeight: 400
    lineHeight: 1.6
  label:
    fontFamily: "Jost, Avenir Next, Segoe UI, system-ui, sans-serif"
    fontSize: ".9rem"
    fontWeight: 500
    letterSpacing: "0.04em"
rounded:
  focus: "6px"
  soon: "20px"
  card: "24px"
  event: "32px"
  pill: "999px"
spacing:
  gutter: "16px"
  wrap: "1180px"
  cluster: "0.75rem"
  pair: "1.25rem"
  stack: "1.4rem"
  block: "3rem"
  section: "clamp(5rem, 3rem + 7vw, 9rem)"
components:
  button-primary:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.sand-50}"
    typography: "{typography.body}"
    rounded: "{rounded.pill}"
    padding: ".45rem .5rem .45rem 1.5rem"
    height: "52px"
  button-primary-on-dark:
    backgroundColor: "{colors.sand-50}"
    textColor: "{colors.ink}"
    rounded: "{rounded.pill}"
    padding: ".45rem .5rem .45rem 1.5rem"
    height: "52px"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.ink}"
    rounded: "{rounded.pill}"
    padding: ".45rem 1.5rem"
    height: "52px"
  button-ghost-on-dark:
    backgroundColor: "transparent"
    textColor: "{colors.dusk-fg}"
    rounded: "{rounded.pill}"
    padding: ".45rem 1.5rem"
    height: "52px"
  rail-card:
    textColor: "{colors.dusk-fg}"
    rounded: "{rounded.card}"
    padding: "1.4rem"
  step-tile:
    textColor: "{colors.dusk-title}"
    rounded: "{rounded.card}"
    padding: "1.8rem"
  event-card:
    backgroundColor: "{colors.sand-50}"
    textColor: "{colors.ink}"
    rounded: "{rounded.event}"
  event-date:
    backgroundColor: "{colors.umber-800}"
    textColor: "{colors.dusk-fg}"
    padding: "2.4rem 2rem"
  coming-soon:
    textColor: "{colors.ink}"
    rounded: "{rounded.soon}"
    padding: "clamp(1.25rem, 1rem + 1.5vw, 2rem)"
  tag-soon:
    textColor: "{colors.muted}"
    rounded: "{rounded.pill}"
    padding: ".15rem .6rem"
  newsletter-field:
    textColor: "{colors.ink}"
    rounded: "{rounded.pill}"
    padding: "6px"
  lang-toggle:
    textColor: "{colors.dusk-fg-2}"
    rounded: "{rounded.pill}"
    padding: "3px"
  lang-toggle-active:
    backgroundColor: "{colors.dusk-fg}"
    textColor: "{colors.umber-900}"
---

# Design System: AVA Art & Soul

<!-- Recorded 2026-10-17 from design/directions/index.html, direction B "Amurg" (the `.dir-b` block, `b-*` classes and shared atoms), chosen by the client on 2026-10-17. -->

## Overview

**Creative North Star: "Light on Sand"**

One world taken straight from the AVA logo: dark-brown line drawing on sand, warmed by a diffuse light that runs from umber through clay to beige, and glowing motes (the "woodsprites") that drift and softly follow the visitor. The home page is an evening at the workshop table: it opens in umber dusk under a full-bleed warm photograph of hands in clay, then lifts through a dawn band into sand as the visitor reads. Elegance comes from restraint and from the type trio (Fraunces for the voice, Jost for the information, Pinyon Script for a handful of handwritten words), not from ornament.

The page runs in four bands: dusk (hero, about, services rail, steps) on `umber-900 → umber-800 → umber-700`; a dawn band `umber-700 → clay-400 → sand-200`; sand (the next event, the Coming soon pair, the newsletter) on `sand-200 → sand-100`; and an `umber-900` footer. Every gap in content is shown honestly with the "În curând / Coming soon" pattern; nothing is invented to fill the layout. Motion is damped and physical, never snapped; bright light is reserved for what moves or is actionable.

Directions A Liniște and C Jurnal were shown and not chosen (2026-10-17); see design/directions/.

**Key Characteristics:**
- Dark brown on sand, from the logo; one warm earth ramp, no second hue.
- Dusk first, lifting to sand: umber bands above, a dawn band, sand below, umber footer.
- Fraunces at light weights (300–400), Jost body, Pinyon Script for the hero tagline and a few words.
- Pill-shaped actions with a circular arrow well; soft, large radii elsewhere.
- Diffuse gradient light and additive woodsprite motes as the only "effects".
- Honest "Coming soon" placeholders instead of invented content.
- Romanian first (ș, ț with comma below), English as a full second version.

## Colors

One earth ramp sampled from the logo, from bright sand through clay to deep umber, with dark brown ink for text on sand and a pale dusk tier for text on umber.

### Primary
- **Logo Ink** (`ink`): the logo colour and the default text and primary-button fill on sand. All logo SVGs in `assets/logo/` use this exact value.
- **Soft Ink** (`ink-soft`): secondary text on sand (leads, event description, sub-copy).

### Secondary
- **Deep Clay** (`clay-600`): the accent as text on sand: the event series line and the text caret. 5.9:1 on `sand-50`, 5.6:1 on `sand-100`, 4.5:1 on `sand-200`.
- **Pale Clay** (`clay-400`): the middle of the dawn band and the scrollbar thumb.
- **Fired Clay** (`clay-500`): a ramp step for non-text marks only; never text on sand (see The Clay Text Rule).

### Tertiary
- **Umber** (`umber-700`, `umber-800`, `umber-900`): the dusk surfaces (`umber-900 → umber-800` at 60% `→ umber-700`), the hero veil, the event date panel (`umber-800`), the footer (`umber-900`) and, on sand, the seats-left line (`umber-700`, 8.4:1 on `sand-50`).
- **Mote Glow** (`glow`): the woodsprite warm family; the canvas draws with its own RGB triplets (core `255,246,226`, halo `255,200,120`).

### Dusk tier (text on umber)
Contrast is WCAG 2.x against each umber step.

| Token | Use | on `umber-900` | on `umber-800` | on `umber-700` |
|---|---|---|---|---|
| **Dusk Paper** (`dusk-fg`) | primary text, nav current, headings, lockup, button text, rail card names | 14.67:1 | 11.87:1 | 8.42:1 |
| **Dusk Linen** (`dusk-fg-2`) | secondary text: nav links, hero lead, about lead, rail lines, date weekday and time, footer | 11.99:1 | 9.70:1 | 6.88:1 |
| **Dusk Straw** (`dusk-fg-3`) | tertiary text: rail hint, footer reply note | 8.29:1 | 6.70:1 | 4.76:1 |
| **Dusk Lamp** (`dusk-accent`) | accent text: script section names, step numerals, script month, links on dusk | 11.84:1 | 9.58:1 | 6.80:1 |
| **Dusk Flame** (`dusk-title`) | the hero tagline and step text, the brightest words | 14.89:1 | 12.04:1 | 8.55:1 |
| **Dusk Hairline** (`dusk-line`) | 1px rules on dusk, decorative only | 1.61:1 | 1.62:1 | 1.52:1 |

Every dusk text colour passes AA for body text (4.5:1) on all three umber steps; the tightest pair is `dusk-fg-3` on `umber-700` at 4.76:1, so tertiary text on the lightest dusk step is close to the floor and must not go smaller than `typography.label`. `dusk-line` fails the 3:1 non-text minimum on every step: it may separate content but must never be the only visible edge of a control or field. None of the tier holds contrast on the dawn band's `clay-400` stop (`dusk-fg-3` is 1.37:1 there); the dawn band carries no text.

### Neutral
- **Bright Sand** (`sand-50`): the event card, button text on ink, the inverted primary on dusk.
- **Sand** (`sand-100`): the lower sand band and the `html` colour.
- **Warm Sand** (`sand-200`): the foot of the dawn band and top of the sand band, image placeholders.
- **Deep Sand** (`sand-300`): text selection.
- **Muted Earth** (`muted`): tertiary text on sand: Coming soon label, `dt` captions, placeholders. 5.5:1 on `sand-100` but 4.4:1 on `sand-200`, so muted text sits on `sand-100` or lighter.
- **Hairline** (`line`): 1px rules and inset rings on sand.
- **Kiln Red** (`error`): the newsletter validation message only.

### Named Rules
**The One Ramp Rule.** Every colour comes from the sand–clay–umber ramp, the ink pair or the dusk tier. There is no second hue; warmth and depth come from moving along the ramp, never from adding a colour.

**The Clay Text Rule.** `clay-500` passes only 3.5:1 on `sand-100` and 2.9:1 on `sand-200`, so accent text on sand uses `clay-600` (≥ 4.5:1 down to `sand-200`). `clay-500` stays for non-text marks.

**The Surface Tier Rule.** Text colour is set by surface tier tokens (`--bg`, `--fg`, `--fg-2`, `--fg-3`, `--line`), and dusk surfaces re-declare the whole tier. Components read the tier, never a raw hex, so the same component works on sand and on dusk.

**The Dusk Tier Rule.** Dusk surfaces (`umber-700` to `umber-900`, the hero veil, the date panel, the footer) use only the dusk tier: `dusk-fg`, `dusk-fg-2`, `dusk-fg-3`, `dusk-accent`, `dusk-title` and `dusk-line`. No other light hex is set on dusk, and ink-tier colours never appear there.

## Typography

**Display Font:** Fraunces (variable, opsz 9–144, wght 300–600, roman and italic), with Iowan Old Style, Palatino Linotype, Georgia
**Body Font:** Jost (wght 300–600), with Avenir Next, Segoe UI, system-ui
**Script Font:** Pinyon Script, with Snell Roundhand, Apple Chancery. Pinyon Script is a free stand-in for Edwardian Script ITC, which the client asked for but which has no web licence yet; swap the family in `--f-script` when one is bought, nothing else changes.

**Character:** A soft, high-contrast old-style serif speaking at light weights carries the voice; a clean geometric sans (the same family as "ART & SOUL" in the logo) carries information; a formal copperplate script appears like a handwritten note, a few words at a time, brightest at the hero.

### Hierarchy
- **Display** (Pinyon Script 400, `typography.display`, line-height .95, `dusk-title`): the hero tagline "autocunoaștere prin creație", under the wordmark.
- **Headline** (Fraunces 350, `typography.headline`, 1.08, -0.015em): section heads (`h2`) on dusk and on sand.
- **Script** (Pinyon Script 400, `typography.script`, 1.05, `dusk-accent`): section names such as "Cine suntem"; also the script month on the date panel (2.6rem) and step numerals (3rem, line-height .8).
- **Title** (Fraunces 400, `typography.title`, 1.1): rail card names; the event title runs `clamp(1.7rem,1.3rem + 1.2vw,2.3rem)`; Coming soon headings use Fraunces 350 at 1.5rem, 1.2.
- **Lead** (Fraunces 350, `typography.lead`, 1.5): sub-copy under heads and the hero lead (1.55, max 44ch); the about statement scales to `clamp(1.35rem,1.1rem + 1vw,1.9rem)`; step text is Fraunces 350 at 1.25rem, 1.4.
- **Body** (Jost 400, 1.0625rem, 1.6): running text, max 42–48ch.
- **Label** (Jost 500, .9rem, +0.04em, sentence case): "În curând", rail hint. The inline status tag uses .75rem.
- **Date numeral** (Fraunces 300, `clamp(5rem,3rem + 5vw,6rem)`, line-height .85, -0.04em) with tabular figures for weekday and time.

### Named Rules
**The Few Words Rule.** Pinyon Script is for two to four words at a time (the hero tagline, a section name, a month, a step numeral). Never body, never buttons, never a full sentence.

**The Light Voice Rule.** Fraunces runs at 300–400. Emphasis comes from size and italic, not weight; 500 belongs to Jost (buttons, labels, links).

**The Comma-Below Rule.** Romanian copy uses ș and ț with comma below (U+0219, U+021B), never the cedilla forms. Every face in the trio must render them; check any replacement script face before adopting it.

## Layout

A single centred column, max `spacing.wrap` (1180px) plus 16px gutters that respect safe-area insets. The page is four full-bleed bands stacked in order: dusk, dawn, sand, footer; content sits in the column inside each band. Sections breathe on `spacing.section` vertical padding; a section that follows a head often trims or drops its top padding to keep the pair together. Inside sections the rhythm is: cluster `0.75rem` between buttons, stack `1.4rem` between head/lead/link, `3rem` from a head to its grid, `1.25rem` between paired cards.

- **Hero:** full-bleed, `min(86svh, 860px)` tall; nav at the top, copy anchored bottom-left (max 860px, gap 1.3rem, bottom padding `clamp(2.5rem,2rem + 3vw,5rem)`).
- **About:** 5/7 split, aligned to the bottom; collapses below 820px.
- **Services rail:** a horizontal scroll-snap rail of five cards, column width `clamp(250px,24vw,330px)`, gap 1rem; from 1212px its start edge aligns with the column. A head row puts the `h2` left and the swipe hint right.
- **Steps:** three tiles across, gap 1rem, one column below 760px.
- **Dawn band:** `clamp(140px,16vw,240px)` tall, no content.
- **Event:** 4/7 split card (date panel / body), one column below 760px.
- **Coming soon pair:** two columns, one below 760px.
- **Newsletter:** centred stack, field max 520px.
- **Footer:** 1.4/1/1 grid, one column below 760px.

Primary nav becomes a menu button below 900px; the newsletter field stacks below 480px. Body copy is held to 42–48ch, leads to 30–46ch. Headings use `text-wrap: balance`, paragraphs `pretty`.

## Elevation & Depth

Depth is light, not shadow. Surfaces are flat and tonal; the felt depth comes from moving along the ramp (dusk to dawn to sand), from the diffuse radial light baked into dark surfaces, and from the three layers of motes floating above the reading plane (the canvas sits at z-index 5, pointer-events none). The hero photograph sits under an umber veil (`umber-900` at the foot, 86% at 30%, 35% at 62%, 55% at the top) with a warm radial at top right (`rgba(255,214,150,.28)`); the date panel carries the same warmth in its top-right corner (`rgba(255,214,150,.4)`, 260px). One shadow exists, to lift the event card off the sand.

### Shadow Vocabulary
- **Event lift** (`box-shadow: 0 40px 80px -40px rgba(42,30,22,.55)`): the event card on sand, the only drop shadow.
- **Inset ring** (`box-shadow: inset 0 0 0 1px color-mix(in oklab, var(--fg) 22–30%, transparent)`): ghost button, language toggle, menu button; borders are drawn as inset rings, not `border`.
- **Tile ring** (`box-shadow: inset 0 0 0 1px rgba(255,248,236,.18)`, fill `rgba(255,248,236,.12)`): the translucent step tiles on dusk.

### Named Rules
**The Light Is Reserved Rule.** Bright, moving light belongs to what moves or is actionable: motes gather at the primary action, nowhere else. Static surfaces may carry only diffuse, low-alpha radial light baked into their background (the hero's top-right warmth, the date panel's corner); never glows, blooms or lens effects on text, cards or images.

**The Still Reading Plane Rule.** Text and cards stay put; only the light layer drifts. Content never parallaxes.

## Shapes

Soft and round, echoing thrown clay. Actions and toggles are full pills (`rounded.pill`) or circles (44px icon wells, 38px arrow wells). Containers use large radii: `rounded.soon` (20px) for Coming soon cards, `rounded.card` (24px) for rail cards and step tiles, `rounded.event` (32px) for the event card; the newsletter field becomes a 26px rounded box when stacked. Focus outlines take `rounded.focus` (6px). Hairline rules (1px `line` on sand, `dusk-line` on dusk) separate content.

## Components

### Buttons
Soft, confident pills with a circular arrow well; never more than one filled button per group.
- **Shape:** full pill (`rounded.pill`), min-height 52px.
- **Primary:** `ink` fill, `sand-50` text, Jost 500, +0.01em; trailing 38px circular well (text colour at 14% mix) holding a 15px line arrow (↗ drawn as inline SVG, 1.4 stroke).
- **Hover / Focus:** the arrow well nudges `translate(3px,-1px) scale(1.05)` over 260ms `ease-out` (fine pointers only); press scales to .97 over 160ms; focus is a 2px currentColor outline, 3px offset. Primary buttons carry `data-glow`: on hover or focus the motes gather around them.
- **Ghost:** transparent with a 1px inset ring at 30% of the text colour, padding `.45rem 1.5rem`, hover fills at 7%.
- **On dusk (hero):** primary inverts to `sand-50` fill and `ink` text; ghost uses `dusk-fg` text and ring.
- **Text link:** Jost 500, underline at 35% opacity (offset .22em, 1px), full opacity on hover, trailing small arrow; on dusk it takes `dusk-accent`.

### Coming Soon (signature)
The honest placeholder for anything the client does not have yet (testimonials, gallery, retreat details, PFA data).
- **Card:** 1px border at 18% of the text colour, `rounded.soon`, 3% tint fill, padding `clamp(1.25rem,1rem + 1.5vw,2rem)`, gap .4rem. On the home page two sit as a pair in the sand band (testimonials, gallery).
- **Content:** label "În curând / Coming soon" (`typography.label`, `muted`), a Fraunces 350 1.5rem heading, one plain sentence (max 42ch) saying what will appear and, where useful, where to look meanwhile (Instagram).
- **Inline tag:** for a single item in a list (e.g. "în pregătire" next to Retreaturi): .75rem Jost 500 pill with a 35% inset ring, in the tier's tertiary colour.
- **No decoration:** no icons, illustrations, skeletons or fake content.

### Services Rail (signature)
Five tall photo cards on dusk, browsed sideways.
- **Card:** aspect 3:4.2, `rounded.card`, photograph filling the card, a bottom scrim (`rgba(30,21,15,.88)` at the foot to transparent at 80%), text at the bottom with 1.4rem padding: name in Fraunces 400 1.7rem `dusk-fg`, one line in Jost .95rem `dusk-fg-2`.
- **Rail:** scroll-snap to card start, horizontal overscroll contained, thin scrollbar in `dusk-fg` at 35%; focusable region labelled by the section head.
- **Hover:** the photo scales to 1.05 over 900ms `ease-out` (fine pointers only).

### Step Tiles
Three translucent tiles on dusk: fill `rgba(255,248,236,.12)` with the tile ring, `rounded.card`, padding 1.8rem, gap 1rem; numeral in script 3rem `dusk-accent`, text in Fraunces 350 1.25rem `dusk-title`.

### Event Card
The next real event, date first, on sand.
- **Card:** `sand-50`, `rounded.event`, the event lift, 4/7 split.
- **Date panel:** `umber-800` with the dusk tier and the corner light; weekday at the top, the date numeral with the script month in `dusk-accent`, tabular time at the foot (weekday and time in `dusk-fg-2`).
- **Body:** title (Fraunces 400), italic series line in `clay-600`, description in `ink-soft`, a facts list (`dt` in `muted`, `dd` in `ink`), the seats line in `umber-700` 500, then the primary button plus the "all events" text link.

### Inputs / Fields
- **Newsletter field:** a pill container (`rounded.pill`, 6px padding, `rgba(255,251,244,.6)` fill, 1px inset `line`) holding a borderless 16px input and the primary button. Below 480px it stacks with a 26px radius and a 48px input.
- **Focus:** the ring thickens to 1.5px `ink` (`:focus-within`).
- **Error:** a polite live-region message under the field in `error`, `aria-invalid` on the input, focus returns to it.

### Navigation
- **Bar:** sits on the hero photo in the dusk tier. Lockup logo left (52px tall, 38px under 900px) in `dusk-fg`, Jost .95rem links in `dusk-fg-2`, current page in `dusk-fg` with a 1px underline; hover draws the underline from the left (scaleX, 260ms `ease-out`).
- **Language toggle:** RO/EN pill group, 3px inset, 40×32 segments, active segment filled with `dusk-fg` on `umber-900` text. RO is default.
- **Mobile:** 44px round menu button (two lines that cross on open) opens a full-screen sheet: `umber-900` at 88% with 22px backdrop blur, `dusk-fg` Fraunces 350 links at `clamp(2rem,8vw,3rem)` that rise 14px in with 45ms stagger; Escape and link tap close it and return focus.

### Footer
`umber-900` band in the dusk tier: lockup and contact block (email, phone, place, reply note in `dusk-fg-3`), legal links, Jost .95rem in `dusk-fg-2`; links underline on hover.

### Woodsprite Light (signature)
A full-viewport canvas of glowing motes over the whole page.
- **Settings:** 44 motes, 60% followers, additive (`lighter`) compositing, alpha .9, size 1.15, core `255,246,226`, halo `255,200,120`. Motes do not respond to scroll.
- **Mote:** a 96px radial texture (core → halo at 30% → transparent) with nine fine curved filaments, rotated slowly; alpha pulses .72–1.
- **Layers:** three depth ranks: far (scale .45, alpha .45, drift .35, stiffness ×.5), mid (.75, .7, .6, ×.8), near (1.1, 1, 1, ×1). Roughly one mote in seven is on the near layer; far is small, dim and slow.
- **Idle drift:** each mote wanders around a home point on a slow Lissajous path and rises gently, wrapping at the edges.
- **Follow:** followers track the pointer (or the last touch), orbiting it at 26–146px, via a damped spring (stiffness 7–16 /s², damping 0.72 of critical). Following stops after 3.5s without pointer movement.
- **Attract:** hovering or focusing a `data-glow` element (primary buttons) pulls followers into an orbit around it at ~0.55× its larger side.
- **Lifecycle:** paused when the tab is hidden; device pixel ratio capped at 2; timestep capped at 50ms.
- **Reduced motion:** a single still frame (simulated one second in, then drawn once); no follow, no attract, no loop.

### Motion
- **Easings:** `ease-out` `cubic-bezier(0.23,1,0.32,1)` for almost everything; `ease-drawer` `cubic-bezier(0.32,0.72,0,1)` reserved for sheets/drawers.
- **Durations:** press 160ms; colour 200ms; small transforms 260–300ms; sheet 280ms; links in sheet 420ms; entrance 900ms; image hover 900ms; hero settle 2.4s.
- **Entrance:** one orchestrated moment per page: nav, wordmark, tagline, lead and buttons rise 18px from blur(6px) to clear, 70ms stagger from 250ms; the hero photo settles from scale 1.06 to 1 over 2.4s.
- **Scroll reveal:** progressive enhancement only (`animation-timeline: view()`), content is visible without it.
- **Reduced motion:** entrances become a 300ms fade; the hero settle and staggered transitions are removed.

### Logo usage
- Lockup (vase + "AVA" + "ART & SOUL") in the nav and footer, coloured by `currentColor` so it follows the surface tier (`dusk-fg` on dusk, ink on sand).
- The wordmark is Fraunces outlines, "ART & SOUL" is Jost spaced caps, the tagline is Fraunces Italic; the vase is a line drawing (stroke 12 / 7 / 6 at full size).
- Hero use: the wordmark alone (`clamp(120px,7vw + 90px,190px)` wide, `dusk-fg`) over the photo, above the script tagline.
- Source files: `assets/logo/` (primary, horizontal, stacked, symbol, stamp), all in `ink`.

## Do's and Don'ts

### Do:
- **Do** use the "În curând / Coming soon" pattern for every missing testimonial, photo, price, date, retreat detail or legal datum; show only facts from the client's content document.
- **Do** keep primary actions in `ink` pills with the arrow well and `data-glow` (inverted to `sand-50` on dusk), at most one filled button per group, the ghost pill beside it for the second door ("Pentru companii").
- **Do** hold text on sand to `ink`, `ink-soft`, `muted` or `clay-600`, and text on dusk to the dusk tier; keep every text pair at WCAG 2.2 AA (4.5:1 body, 3:1 large) and recheck when a gradient stop sits behind text.
- **Do** honour `prefers-reduced-motion` for every animation, including the woodsprite canvas (still frame, no follow).
- **Do** write Romanian with comma-below ș and ț, and test every font (especially the script) with them.
- **Do** draw borders as 1px inset rings or hairlines (`line` on sand, `dusk-line` on dusk), and use `rounded.pill` for anything clickable that is not a card.

### Don't:
- **Don't** invent testimonials, prices, dates, client logos or photos, and don't fill content gaps with decoration.
- **Don't** set Pinyon Script for more than a few words, for body text, buttons or labels.
- **Don't** introduce a hue outside the sand–clay–umber ramp, use `clay-500` for text on sand (use `clay-600`), or set a light hex on dusk that is not in the dusk tier.
- **Don't** put glows, blooms or motion on static text, cards or images; bright light belongs to the motes and the primary action, and static surfaces get only diffuse radial light.
- **Don't** use hard or dark neutral shadows; the one shadow is long, soft and umber-tinted.
- **Don't** ship the bottom review switcher pill (A · Liniște / B · Amurg / C · Jurnal); it is mockup chrome for the client review, not part of the site.
