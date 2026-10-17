# SEO plan

## Foundations
- Server-rendered/static HTML for every page; one `<h1>` per page.
- `generateMetadata` per page and locale: unique `<title>` (≤ 60 chars, pattern `{Page} — AVA Art & Soul`) and meta description (≤ 155 chars) written from the page's real copy.
- `alternates.languages`: `ro-RO` ↔ `en` + `x-default` → RO. Canonical per locale.
- `app/sitemap.ts` (both locales, `lastModified` from Sanity), `app/robots.ts`. Payment result pages `noindex`.
- Open Graph + Twitter cards per page; OG images generated with `next/og` in the brand style (logo on sand), RO and EN.
- `<html lang="ro">` / `lang="en"`.
- Clean slugs (see `sitemap.md`), breadcrumbs on service and event pages.

## Structured data (JSON-LD)
| Page | Types |
|---|---|
| All | `Organization` (name, logo, sameAs Instagram, email, telephone) |
| Home, Contact | `LocalBusiness` (address only once a fixed address is confirmed for publication; areaServed București) |
| Event detail | `Event` (name, startDate, duration, location, offers with price RON + availability, organizer, performer = facilitators) |
| Service pages | `Service` + `Offer` (only real prices) |
| FAQ blocks | `FAQPage` |
| About | `Person` for Alessia (jobTitle: "Consilier în dezvoltare personală", never "psiholog") |
| Breadcrumbs | `BreadcrumbList` |

## Keywords (RO first, from real services)
ateliere de ceramică București · atelier modelaj lut Cotroceni · atelier lut pentru adulți · teambuilding ceramică București · ateliere wellbeing companii · consiliere dezvoltare personală București / online · atelier lut copii · Școala Altfel ateliere lut · voucher cadou atelier ceramică · retreat creativ (later).
EN: pottery workshop Bucharest · clay workshop Bucharest · team building pottery Bucharest.

## Content that earns ranking
- Event pages stay live after the event as archive pages (with photos), not deleted.
- Each service page answers its FAQ in visible text (also feeds `FAQPage`).
- Alt text on every image, in both languages, describing the actual photo.
- Google Business Profile for the studio (client task), linked from the site.

## Performance (Core Web Vitals targets)
LCP < 2.0 s on 4G, CLS < 0.05, INP < 200 ms. Hero image via `next/image` with `priority` and AVIF/WebP; fonts self-hosted with `display: swap` and subsetting (latin + latin-ext for ș/ț); the woodsprite canvas starts after first paint and never blocks LCP.
