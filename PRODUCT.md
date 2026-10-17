# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Next.js (App Router) on Vercel, chosen by the user on 2026-10-17. Sanity as the admin for content the client edits (events, gallery, testimonials, team, FAQ), Stripe for payments (RON, payouts to the client's ING Business account), Cal.com + Stripe for 1:1 bookings, Brevo for the newsletter. Vercel Hobby is non-commercial only, so launch needs the Pro plan.

## Users

Two paths, and the home page must show both immediately:

1. **Individuals** (mostly adults, sometimes parents booking for a child aged 5+) who want something for themselves: a monthly group clay workshop, a private 1:1 clay workshop, 1:1 personal-development counselling, or a retreat. Most have never touched clay. Many come alone. Situation: tired, curious, looking for a calm, safe way to reconnect with themselves.
2. **Companies** (HR, team leads) looking for teambuilding or wellbeing workshops for teams of 4 to 16, at their office or a partner venue, invoiced through the PFA. They ask for a custom quote.

Secondary: schools and kindergartens ("Școala altfel / Săptămâna verde"), artists and entrepreneurs who want to co-host a workshop.

## Product Purpose

AVA Art & Soul ("autocunoaștere prin creație") runs clay workshops, counselling and retreats in București (Cotroceni). The site has to make a visitor understand within 30 seconds who they are, what they do and where to click to sign up, then let them sign up and pay online. Success: people find the right service, book and pay without writing a DM, and join the newsletter.

## Positioning

Clay is the tool, not the point. While the hands work, the mind settles and people talk more honestly. The founder, Alessia Văideanu, is a ceramic artist and accredited personal-development counsellor (Sandonia Institute, 2026), with a Psychology degree (Universitatea Transilvania Brașov, 2026) and a master's in progress in experiential psychotherapy and personal development (FPSE, Universitatea din București). Small groups (max 12) keep it intimate.

## Operating Context

- Monthly themed group workshops (2 h, sometimes with guest artists), private 1:1 workshops (90 min), counselling (60–90 min, online or in person, free 15-min intro call), company workshops, school workshops, retreats (in preparation).
- Pieces are dried and fired; collected 4–6 weeks later.
- Bookings currently via DMs / Google Forms; moving to online payment on the site.
- The client updates events at least monthly; past events go to an archive.
- Romanian is the default language; English is a full second version.

## Capabilities and Constraints

- Pages: Acasă · Despre noi · Ce facem (Ateliere de grup, Pentru companii, Consiliere 1:1, Atelier privat 1:1, Retreaturi, Pentru școli și copii) · Evenimente · Galerie · Contact; footer: FAQ, Înscrieri/plată/anulare, Termeni, Confidențialitate, Cookies, ANPC, PFA data, Instagram.
- Online payment for group workshops/events, private 1:1, gift vouchers and counselling.
- Newsletter (Brevo, double opt-in) with a pop-up: 5% discount at the next event for subscribers.
- Good SEO is a requirement (RO + EN, hreflang, structured data).
- **Legal wording:** never "psiholog", "psihoterapeut", or "terapie / art-terapie" as a service. Services are "consiliere în dezvoltare personală" and "autocunoaștere prin artă". Counselling does not replace psychotherapy or medical treatment.
- Cancellation policy: seat confirmed only after full payment; no refunds, but 24 h notice moves the seat to the next workshop. Retreats need separate rules (undecided).
- Undecided: domain (avceramic.com or new), domain email, PFA identification data, retreat details, legal texts.

## Brand Commitments

- Name: AVA Art & Soul. Tagline: "autocunoaștere prin creație".
- Logo (from `Identitate · Logo.pdf`): line-drawn clay vase with two bands; serif "AVA"; "ART & SOUL" in spaced sans caps; italic serif tagline; round ceramic stamp. Dark brown on sand. Redrawn as SVG in `assets/logo/`.
- The client asked for: elegance, calm, richness; a diffuse gradient light from beige to light brown; a glowing light like the woodsprites in Avatar that softly follows the visitor; Edwardian Script ITC where it fits (replaced by a free lookalike, Pinyon Script, until a web licence is bought).
- Voice: warm, plain, second person singular ("tu"), never clinical, never salesy.

## Evidence on Hand

- All page copy, prices and FAQ: Claude Doc "AVA Art & Soul — Conținut și structură site", mirrored in `docs/content/ro.md`.
- Prices: group workshops from 185 lei/person; counselling 150 lei/hour; private 1:1 250 lei adult / 220 lei child / 450 lei for 2; schools 45 lei/50 min/child; companies on request.
- Next event: "Modelaj în lut & Scriere creativă (Pauză de Suflet — ediția 2)", Sunday 15 November 2026, 18:00 (2 h 30), Cotroceni, 200 lei.
- Team photos: Iuliana Petrescu, Casandra Samargiu (`assets/photos/team/`). Alessia's photo: pending.
- **Absent, must not be fabricated:** testimonials, company/partner logos, HR testimonial, retreat dates/prices/programme, workshop photos, PFA data, past-event archive. Show "În curând / Coming soon" instead.

## Product Principles

1. Two doors, always visible: "for you" and "for your team".
2. Every service page follows the same template: for whom, what happens, what you get, who facilitates, duration/price/place, FAQ, sign-up button.
3. Truth over polish: nothing is invented; gaps are labelled "Coming soon", cleanly.
4. Safety first: the tone and wording make people feel in good hands, and stay legally correct.
5. Booking without friction: from interest to paid seat in as few steps as possible.

## Accessibility & Inclusion

WCAG 2.2 AA. All motion (including the woodsprite light) respects `prefers-reduced-motion`. Romanian diacritics (ș, ț with comma below) must render in every font.
