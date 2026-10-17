# AVA Art & Soul — website

Bilingual (RO default, EN) brand site for AVA Art & Soul: clay workshops, personal-development counselling, private 1:1 workshops, company workshops, retreats. Bucharest, Cotroceni.

## Read first
- `PRODUCT.md` — who it's for, positioning, constraints, evidence on hand
- `DESIGN.md` — visual system (tokens, type, motion, woodsprite light, placeholders)
- `docs/content/ro.md` — all copy (source of truth); `docs/content/en.md` — draft translation
- `docs/sitemap.md` · `docs/architecture.md` · `docs/seo.md` · `docs/legal.md` · `docs/missing-content.md`
- `docs/superpowers/specs/` — design spec(s); `docs/superpowers/plans/` — build roadmap and milestone plans
- Chosen design: direction B "Amurg" (dusk → dawn → sand). Home page contract: `.impeccable/surfaces/src-views-homepage-tsx.md`

## Hard rules
1. **Never invent** testimonials, prices, dates, numbers, clients, or facts. Missing → "În curând" / "Coming soon" in the clean placeholder style from DESIGN.md. No random decoration.
2. **Wording:** never "psiholog", "psihoterapeut", "terapie" or "art-terapie" as a service. Use "consiliere în dezvoltare personală", "autocunoaștere prin artă".
3. **Romanian first.** Every user-facing string exists in RO and EN. Diacritics with comma below: ș ț Ș Ț (never ş ţ).
4. **Git:** never commit, branch or push. The client's developer commits.
5. Every animation respects `prefers-reduced-motion`.
6. Placeholder photos live in `assets/photos/placeholder/` (see CREDITS.md) and must be replaced before launch.

## Stack (decided)
Next.js App Router on Vercel (Pro at launch) · Sanity admin · Stripe Checkout (RON → ING Business) · Cal.com + Stripe for 1:1 · Brevo newsletter. Details in `docs/architecture.md`.

## Assets
- `assets/logo/` — SVGs redrawn from `source-identitate-logo.pdf` (Fraunces + Jost outlines): symbol, primary (with tagline), stacked, horizontal, stamp
- `assets/photos/team/` — Iuliana Petrescu, Casandra Samargiu. Alessia's photo pending.
- `design/directions/` — the 3 home-page direction mockup (published as a claude.ai artifact). Open `preview.html` through any static server (e.g. `python3 -m http.server -d design/directions`).

## Skills to use, by phase
- Plan: `superpowers:brainstorming` → `superpowers:writing-plans` → `superpowers:executing-plans` / `subagent-driven-development`
- Design: `impeccable` (shape, critique, audit, polish), `frontend-design`, `taste-skill:high-end-visual-design`, `apple-design`
- Motion: `animate`, `emil-design-eng`, `review-animations`, `mobile-native`
- Code: `vercel-react-best-practices`, `vercel-composition-patterns`
- Test: `playwright-cli`, `webapp-testing`, `chrome-devtools-mcp:a11y-debugging`, `debug-optimize-lcp`
- Before launch: `security-review`, `find-security-vulnerabilities-in-code` (forms + payments), `superpowers:verification-before-completion`
