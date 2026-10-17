# Architecture (production build)

Decided with the client on 2026-10-17. Built in the next milestone, after a design direction is chosen.

## Stack
| Concern | Choice | Notes |
|---|---|---|
| Framework | Next.js (App Router, TypeScript) | Static generation + ISR for content pages |
| Hosting | Vercel | **Pro plan needed at launch**: Hobby is non-commercial only |
| Content admin | Sanity (free tier) | Client edits events, gallery, testimonials, team, FAQ, in RO + EN |
| Payments | Stripe Checkout (RON) | Payouts to the client's ING Business account. Cards + Apple Pay / Google Pay |
| 1:1 booking | Cal.com embed + Stripe | Counselling (60/90 min), private workshop (90 min), free 15-min intro call |
| Newsletter | Brevo | Double opt-in, list per language, "5% next event" pop-up |
| Email (transactional) | Stripe receipts + Brevo transactional | Booking confirmation with full details |
| Analytics | Vercel Web Analytics (cookieless) | Avoids a cookie banner for analytics; banner still needed if Meta pixel etc. is added |
| Fonts | Self-hosted via `next/font` | Fraunces, Jost, Pinyon Script (see DESIGN.md) |

## i18n
- Route groups: `app/(ro)/…` at root, `app/en/…` for English, or `app/[locale]` with `ro` rewritten to `/`. Keep slugs per locale (see `sitemap.md`).
- UI strings in `messages/ro.json`, `messages/en.json`. Sanity documents use field-level localisation (`title.ro`, `title.en`).
- Language switch keeps the user on the equivalent page.

## Sanity schemas
- `event`: title, slug, theme, description, startsAt, durationMinutes, venueArea (public), venueAddress (sent after booking), priceRon, capacity, facilitators[], image, status (scheduled / soldOut / cancelled / past), gallery[] (for archive), stripePriceId (or price built server-side)
- `service`: the six service pages, each section of the template as fields
- `teamMember`: name, role, bio, photo, order
- `testimonial`: text, displayName (first name / initial / anonymous), service ref, consentGiven (required true to publish), date
- `galleryItem`: image, category (ateliere / piese / retreaturi), alt, consentGiven
- `faq`: question, answer, scopes[] (home, group, companies, counselling, private, retreat, schools, events, general)
- `voucher`: product definitions (which service, value)
- `siteSettings`: contact, socials, PFA data, newsletter copy, announcement

## Payments flow (events / group workshops)
1. "Mă înscriu" → server action creates a Stripe Checkout Session (RON, price from Sanity, metadata: eventId, locale, photo-consent flag, newsletter opt-in).
2. Seats: before creating the session, check `capacity − paid bookings − open holds`; hold a seat for the session lifetime (30 min).
3. Stripe webhook `checkout.session.completed` → record booking (Sanity or a small Postgres table), decrement seats, send confirmation with exact address.
4. `checkout.session.expired` → release hold.
5. Sold out → "Listă de așteptare" form instead of the button.
- Terms checkbox + link to cancellation policy before paying (required, see `legal.md`).
- Discount: Brevo subscribers get a 5% Stripe promotion code at the next event.

## Payments flow (1:1)
Cal.com event types with Stripe payment enabled: "Consiliere 60 min", "Consiliere 90 min" (150 lei/hour, so 90 min price to be confirmed by client), "Atelier privat adult / copil / 2 persoane", "Discuție de cunoaștere 15 min (gratuit)". Embedded inline on the service pages.

## Gift vouchers
Stripe Checkout one-off product per voucher type; webhook emails a PDF/HTML voucher with a code; the client redeems manually (or via Stripe promotion code). Voucher values: only the existing prices until the client defines others.

## Forms
Contact and company-quote forms → server action → Brevo transactional email to ava.events.26@gmail.com + autoreply. Spam: honeypot + Vercel BotID / Turnstile. GDPR checkbox required.

## Security & privacy
Stripe webhook signature verification; secrets only in Vercel env vars; counselling bookings collect the minimum data (no health details in forms). Run `security-review` and a Strix scan before launch (forms + payments).
