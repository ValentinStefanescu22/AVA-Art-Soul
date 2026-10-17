# AVA Art & Soul — build roadmap (direction B "Amurg")

**Spec:** `docs/superpowers/specs/2026-10-17-ava-website-design.md` · **Design:** `DESIGN.md` (direction B) · **Contract:** `.impeccable/surfaces/src-views-homepage-tsx.md` · **Copy:** `docs/content/ro.md`, `docs/content/en.md` · **Architecture:** `docs/architecture.md`

The build has five independent subsystems, so it gets five plans, written one at a time. Each milestone leaves a site that builds, passes its tests and can be previewed on Vercel. Only M1 is planned in detail now; each later plan is written when its milestone starts, against the code that exists then.

| # | Milestone | Delivers | Plan | Needs from the client first |
|---|---|---|---|---|
| M1 | Site foundation | Next.js app, Amurg design system, woodsprite light, RO/EN routing, every content page from typed content files, forms with validation (not yet sending), SEO metadata, sitemap, JSON-LD | `2026-10-17-m1-site-foundation.md` | Nothing. Uses placeholder photos and "În curând" where content is missing |
| M2 | Sanity admin | Events, gallery, testimonials, team, FAQ, site settings editable in RO + EN; on-demand revalidation | written at M2 start | A Sanity account owned by the client |
| M3 | Payments | Stripe Checkout (RON) for events and gift vouchers, seat holds and counts, webhook, confirmation email with the exact address, sold-out waiting list | written at M3 start | Stripe account verified with the ING Business IBAN; voucher types and values; decision on where bookings are stored (Sanity transactions or Postgres) |
| M4 | 1:1 bookings and messages | Cal.com embeds with Stripe for counselling (60/90 min), private workshop (adult / child / 2 people) and the free 15-min intro call; Brevo newsletter with double opt-in and the 5% pop-up; contact and company-quote forms sending email | written at M4 start | Cal.com and Brevo accounts; price of a 90-min counselling session |
| M5 | Legal and launch | Terms, privacy, cookies, booking/cancellation pages, ANPC links, PFA footer data; accessibility, performance and security reviews; domain; Vercel Pro | written at M5 start | PFA data, reviewed legal texts, domain, real photos |

Order: M1 → M2 → M3 → M4 → M5. M3 and M4 touch different files and can run in parallel once M2 is merged.

## Rules for every milestone
- Never commit, branch or push. Each task ends with a checkpoint that lists the changed files; the client's developer commits.
- Never invent testimonials, prices, dates or facts. Missing content renders the "În curând / Coming soon" component.
- Never "psiholog", "psihoterapeut", "terapie" or "art-terapie" as a service name, title or meta text.
- Romanian first, ș ț with comma below. Every string in both locales.
- Every animation respects `prefers-reduced-motion`.
- Each milestone ends with `superpowers:verification-before-completion`; M1 also ends with the impeccable finish review (the contract's FINISH line).
