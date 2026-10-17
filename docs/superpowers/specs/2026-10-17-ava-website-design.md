# AVA Art & Soul website — design spec

Date: 2026-10-17 · Status: direction B "Amurg" chosen by the client on 2026-10-17 (A and C kept in `design/directions/` for reference)

## Intent
A calm, elegant, rich site for AVA Art & Soul ("autocunoaștere prin creație") that, within 30 seconds, tells a visitor who they are, what they offer and where to click, then lets them book and pay online. Two doors from the first screen: "for you" (workshops, counselling, private 1:1, retreats) and "for your team" (companies).

## Goals
- Online booking and payment for group workshops/events, private 1:1 workshops, gift vouchers and counselling.
- Strong local SEO in Romanian, full English version.
- Newsletter with a 5% next-event incentive.
- The client updates events, gallery and testimonials herself.

## Non-goals (for launch)
- Online courses, shop for ceramics, member accounts.

## Anti-goals (failure even if it works)
- Anything invented: testimonials, prices, dates, client logos.
- Clinical or therapy wording ("psiholog", "terapie").
- Template look; decoration filling gaps where content is missing.
- Motion that distracts, or that ignores reduced-motion.

## Constraints
- Brand from `Identitate · Logo.pdf`: vase symbol, Fraunces "AVA", Jost spaced caps, Fraunces italic tagline, dark brown on sand.
- Client's visual brief: elegance, calm, rich; diffuse beige → light-brown gradient light; woodsprite-like glowing motes (Avatar) that softly follow the visitor; Edwardian Script ITC where it fits → Pinyon Script (free) until a licence is bought.
- Legal: Legea 365/2002 footer data, GDPR, ANPC, cancellation policy (see `docs/legal.md`).

## Decided by the client
Stack Next.js/Vercel, Sanity, Stripe (→ ING Business), Cal.com + Stripe, Brevo; RO default with EN drafted by us; logo redrawn as SVG; photo identities (Iuliana: beige-coat street photo; Casandra: park photo); three directions to compare: A "Liniște", B "Amurg", C "Jurnal".

## The three directions
- **A · Liniște (quiet):** centred logo lockup on an airy sand gradient that warms toward light brown at the bottom; one framed warm photo; a few slow motes that drift and gather near the primary button on hover.
- **B · Amurg (dusk):** full-bleed warm photo under a deep umber-to-sand gradient veil; richer browns; brighter, more numerous motes in three depth layers; script headline large.
- **C · Jurnal (journal):** editorial split layout; arched photo masked to the vase's silhouette; paper grain; motes respond to scroll; dated event card leads like a journal entry.

Shared across all three: the woodsprite light (canvas, 3 depth layers, damped spring follow, idle drift, touch-follow on phones, static glow under reduced motion, paused while the tab is hidden), the logo, the type trio (Fraunces, Jost, Pinyon Script), the "Coming soon" placeholder pattern, RO/EN toggle.

### Raises taken from the concept round (discipline, not looks)
- From a night-flight instrument panel: motion is damped and physical, never snapped.
- From a cracktro title screen: depth is rank — motes live on three layers (far ones smaller, dimmer and slower, like parallax); the reading plane stays still.
- From a paper automaton: the glow is reserved for what's in motion or actionable (motes gather at the primary action).
- From a brine calendar: the date is the primary structure of event cards.

## Left to the builder
Exact spacing scale, component details, Sanity schema field names, test setup — within DESIGN.md and `docs/architecture.md`.

## Next
Build per `docs/superpowers/plans/2026-10-17-ava-build-roadmap.md`, starting with M1 (`2026-10-17-m1-site-foundation.md`).
