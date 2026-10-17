# M1 · Site Foundation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** A bilingual (RO default, EN) Next.js site in the Amurg direction with every content page, the woodsprite light, working validation on forms, and complete SEO metadata, built from typed content files.

**Architecture:** Next.js App Router with two root layouts in route groups: `(ro)` serves `/…` with `<html lang="ro">`, `(en)` serves `/en/…` with `<html lang="en">`. Page files are thin: each renders a shared view from `src/views/` with a `locale`. All copy lives in `src/content/ro.ts` and `src/content/en.ts` (EN is typed as the RO shape, so missing keys fail `tsc`); language-neutral facts (prices, dates, contact) live once in `src/content/facts.ts`. Styling is plain CSS: tokens from DESIGN.md in `src/styles/tokens.css`, CSS Modules per component. M2 will swap the content functions' internals for Sanity without changing their signatures.

**Tech Stack:** Next.js 16.4, React 19.3, TypeScript, CSS Modules, `next/font/google`, `next/image`, Vitest 5 (pure logic), Playwright 1.64 (browser). No UI or i18n library.

**Spec:** `docs/superpowers/specs/2026-10-17-ava-website-design.md`, with `DESIGN.md` (direction B), `.impeccable/surfaces/src-views-homepage-tsx.md` (direction contract), `docs/content/ro.md` + `docs/content/en.md` (copy), `docs/sitemap.md` (pages, URLs, home blocks, service template), `docs/seo.md`.

## Global Constraints
- Never run `git commit`, `git branch`, `git push`. Each task ends with a checkpoint; leave changes for the user.
- Copy comes only from `docs/content/ro.md` / `en.md`. Text marked `⟨ÎN CURÂND⟩` renders `<ComingSoon>`; no invented testimonials, prices, dates, logos, photos.
- Forbidden in any service name, page title or meta description: `psiholog`, `psihoterapeut`, `terapie`, `art-terapie`, `therapy`. `psiholog`/`psihoterapeut` are forbidden everywhere.
- Romanian uses ș ț Ș Ț (U+0219, U+021B, U+0218, U+021A); the cedilla forms ş ţ Ş Ţ must not appear.
- Fonts: Fraunces (variable, opsz + italic), Jost (variable), Pinyon Script 400; subsets `latin` + `latin-ext`.
- Every animation respects `prefers-reduced-motion`; content is visible without JavaScript.
- No horizontal scroll at 320px and 375px widths.
- Event times are Europe/Bucharest. Prices are whole lei, shown as `185 lei`.
- Site origin comes from `NEXT_PUBLIC_SITE_URL` (domain undecided), default `http://localhost:3000`.
- Placeholder photos come from `assets/photos/placeholder/` (keep `CREDITS.md` next to them in `public/img/placeholder/`).

## Review Focus
1. **The only event has passed** (after 15 Nov 2026): Home and Events must show the "next event in preparation" Coming soon card, never a past date with a "Mă înscriu" button, and must not stay stale after a static build. Tested in Task 2 (`nextEvent`), Task 7 (e2e asserting whichever state today's date implies) and Task 9 (past event page); pages that depend on today's date use `export const revalidate = 3600`.
2. **Switching language on a deep page** (a service or an event): the switch must land on the same page in the other language, not on the home page. Tested in Task 5.
3. **JavaScript disabled or failed**: all text, navigation links (footer) and photos must still be visible; nothing waits at `opacity: 0`. Tested in Task 10.
4. **Romanian diacritics in every face**, especially Pinyon Script on the hero tagline: no fallback glyphs. Tested in Task 10 (`document.fonts.check`) and Task 3 (no cedilla forms in content).
5. **Hostile or malformed form input** (empty, 10 000 characters, HTML, missing GDPR consent): rejected with a field message, never echoed as HTML. Tested in Task 8.

---

## File structure

```
src/
  app/
    (ro)/layout.tsx  page.tsx  despre-noi/  ce-facem/  ce-facem/[service]/  evenimente/  evenimente/[slug]/
         galerie/  contact/  intrebari-frecvente/  not-found.tsx  [...missing]/page.tsx
    (en)/en/layout.tsx  page.tsx  about/  what-we-do/  what-we-do/[service]/  events/  events/[slug]/
         gallery/  contact/  faq/  not-found.tsx  [...missing]/page.tsx
    sitemap.ts  robots.ts  icon.svg
  content/   types.ts  facts.ts  ro.ts  en.ts  index.ts
  i18n/      routes.ts
  lib/       format.ts  seo.ts  jsonld.ts  woodsprites.ts  forms.ts
  actions/   forms.ts
  styles/    tokens.css  globals.css
  components/ Section, Button, ComingSoon, Logo, SiteNav, MobileMenu, LangSwitch, Footer,
              Woodsprites, ServiceRail, Steps, EventCard, FaqList, NewsletterForm, ContactForm, JsonLd
              (each Name.tsx + Name.module.css where it has styles)
  views/     HomePage, AboutPage, ServicesPage, ServicePage, EventsPage, EventPage,
             GalleryPage, ContactPage, FaqPage, NotFoundPage
public/img/  placeholder/*.webp + CREDITS.md, team/*.webp, logo/*.svg
tests/unit/*.test.ts   tests/e2e/*.spec.ts
vitest.config.ts  playwright.config.ts
```

---

### Task 1: Scaffold the app and test tooling

**Files:**
- Create: the Next.js project at the repo root (keep existing `docs/`, `assets/`, `design/`, `*.md`), `vitest.config.ts`, `playwright.config.ts`, `tests/unit/smoke.test.ts`, `tests/e2e/smoke.spec.ts`
- Copy: `assets/photos/placeholder/*` → `public/img/placeholder/`, `assets/photos/team/*` → `public/img/team/`, `assets/logo/*.svg` → `public/logo/`, `assets/logo/ava-symbol.svg` → `src/app/icon.svg`
- Modify: `.gitignore` (add `.next/`, `node_modules/`, `playwright-report/`, `test-results/`, `.env*.local`)

**Interfaces:**
- Produces: `npm run dev`, `npm run build`, `npm test` (vitest run), `npm run e2e` (playwright test), `npm run typecheck` (tsc --noEmit).

- [ ] **Step 1:** In a temp dir run `npx create-next-app@16.4.2 ava --ts --app --src-dir --eslint --no-tailwind --import-alias "@/*" --use-npm`, then move its files into the repo root without overwriting existing files. Delete the starter `src/app/layout.tsx`, `page.tsx`, `page.module.css`, `globals.css` (Task 4 and 5 recreate layouts per locale).
- [ ] **Step 2:** `npm i -D vitest@5.0.5 @playwright/test@1.64.1 && npx playwright install chromium`. Add the scripts above, with `"e2e": "next build && playwright test"`. `playwright.config.ts`: `webServer: { command: 'npm run start -- -p 3100', port: 3100, reuseExistingServer: true }`, `use.baseURL: 'http://localhost:3100'`, projects `desktop` (1280×800) and `mobile` (`devices['Pixel 7']`). `vitest.config.ts`: `environment: 'node'`, `include: ['tests/unit/**/*.test.ts']`, alias `@` → `./src` (Playwright reads the tsconfig `paths` itself).
- [ ] **Step 3:** Write `tests/unit/smoke.test.ts` asserting `1 + 1 === 2`, and `tests/e2e/smoke.spec.ts` asserting `GET /robots.txt` returns 200 (fails until Task 9; mark it `test.fixme` now, Task 9 removes the fixme).
- [ ] **Step 4:** Run `npm test` → 1 passed. Run `npm run typecheck` → no errors.
- [ ] **Step 5: Checkpoint.** `git status` lists the scaffold, configs, `public/` copies. Do not commit.

---

### Task 2: Facts and formatting

**Files:**
- Create: `src/content/facts.ts`, `src/lib/format.ts`
- Test: `tests/unit/format.test.ts`

**Interfaces:**
- Produces:
  - `facts` (as const): `contact: { email: 'ava.events.26@gmail.com', phone: '0730 301 996', phoneIntl: '+40730301996', instagram: 'https://www.instagram.com/ava.art.soul/', instagramHandle: '@ava.art.soul' }`, `area: 'Cotroceni, sector 5'`, `groupAddress: 'Strada Elefterie 31, Cotroceni, București'`, `prices: { groupFrom: 185, counsellingHour: 150, privateAdult: 250, privateChild: 220, privatePair: 450, schoolPerChild50: 45 }`, `events: EventFacts[]` with one item `{ slug: 'pauza-de-suflet-2', startsAt: '2026-11-15T18:00:00+02:00', durationMinutes: 150, priceRon: 200, seatsLeft: 6 }`.
  - `type EventFacts = { slug: string; startsAt: string; durationMinutes: number; priceRon: number; seatsLeft: number | null }`
  - `formatPrice(lei: number): string`
  - `eventDateParts(iso: string, locale: Locale): { weekday: string; day: string; month: string; year: string; time: string }`
  - `formatDuration(minutes: number, locale: Locale): string`
  - `nextEvent<T extends { startsAt: string }>(events: readonly T[], now: Date): T | undefined`

- [ ] **Step 1: Write the failing tests**

```ts
expect(formatPrice(185)).toBe('185 lei')
expect(eventDateParts('2026-11-15T18:00:00+02:00', 'ro')).toEqual({ weekday: 'Duminică', day: '15', month: 'noiembrie', year: '2026', time: '18:00' })
expect(eventDateParts('2026-11-15T18:00:00+02:00', 'en')).toEqual({ weekday: 'Sunday', day: '15', month: 'November', year: '2026', time: '6:00 pm' })
// the server may run in UTC: parts must still be Bucharest time
expect(eventDateParts('2026-11-15T23:30:00+02:00', 'ro').day).toBe('15')
expect(formatDuration(150, 'ro')).toBe('2 h 30 min')
expect(formatDuration(120, 'en')).toBe('2 h')
const evs = [{ startsAt: '2026-11-15T18:00:00+02:00' }, { startsAt: '2026-12-13T18:00:00+02:00' }]
expect(nextEvent(evs, new Date('2026-11-01T00:00:00Z'))).toBe(evs[0])
expect(nextEvent(evs, new Date('2026-11-15T17:00:00Z'))).toBe(evs[1])   // started at 16:00Z → no longer "next"
expect(nextEvent(evs, new Date('2027-01-01T00:00:00Z'))).toBeUndefined()
expect(nextEvent([...evs].reverse(), new Date('2026-11-01T00:00:00Z'))).toBe(evs[0]) // unsorted input
```

- [ ] **Step 2:** `npx vitest run tests/unit/format.test.ts` → FAIL (module not found).
- [ ] **Step 3:** Implement with `Intl.DateTimeFormat` (`timeZone: 'Europe/Bucharest'`, locales `ro-RO` / `en-GB`, `hour12: true` for EN); capitalise the first letter of the weekday. `nextEvent` returns the earliest event whose start is after `now`.
- [ ] **Step 4:** Run the test → PASS.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 3: Routes and content

**Files:**
- Create: `src/i18n/routes.ts`, `src/content/types.ts`, `src/content/ro.ts`, `src/content/en.ts`, `src/content/index.ts`
- Test: `tests/unit/routes.test.ts`, `tests/unit/content.test.ts`

**Interfaces:**
- Consumes: `facts`, `formatPrice` (Task 2).
- Produces:
  - `type Locale = 'ro' | 'en'`; `locales: readonly Locale[]`
  - `type StaticPage = 'home' | 'about' | 'services' | 'events' | 'gallery' | 'contact' | 'faq'`
  - `type ServiceKey = 'group' | 'companies' | 'counselling' | 'private' | 'retreats' | 'schools'`
  - `type RouteTarget = { page: StaticPage } | { service: ServiceKey } | { event: string }`
  - `pathFor(target: RouteTarget, locale: Locale): string`
  - `alternatesFor(target: RouteTarget): Record<Locale, string>`
  - `serviceKeyFromSlug(slug: string, locale: Locale): ServiceKey | undefined`
  - `allTargets(): RouteTarget[]` (every page, service and event)
  - `type Dictionary` (= the shape of `ro`), `getDictionary(locale: Locale): Dictionary`
  - Dictionary sections used by later tasks: `nav` (labels per `StaticPage`), `home` (hero, about, services intro, steps[3], nextEvent heading, noEvent card, voices, gallery, newsletter, faq), `services: Record<ServiceKey, ServiceContent>`, `about` (story paragraphs, founder bio + training list, team[2], values), `events: Record<string, EventCopy>`, `eventsPage`, `galleryPage`, `contactPage` (fields, interests[7], gdpr, reply), `faqPage`, `forms` (messages per error key), `comingSoon` (label), `footer`, `meta: Record<page or service, { title: string; description: string }>`
  - `ServiceContent = { name: string; line: string; intro: string; forWhom: string[]; whatHappens: string[]; includes: string[]; facilitator: string; facts: { label: string; value: string }[]; faq: { q: string; a: string }[]; cta: string; image: string; soon?: boolean }`
  - `EventCopy = { title: string; series: string; description: string; includes: string; facilitators: string; cta: string }`

URL map (from `docs/sitemap.md`): home `/` · `/en`; about `/despre-noi` · `/en/about`; services `/ce-facem` · `/en/what-we-do`; service `/ce-facem/{slug}` · `/en/what-we-do/{slug}` with slugs group `ateliere-de-grup`/`group-workshops`, companies `pentru-companii`/`for-companies`, counselling `consiliere`/`counselling`, private `atelier-privat`/`private-workshop`, retreats `retreaturi`/`retreats`, schools `scoli-si-copii`/`schools`; events `/evenimente` · `/en/events`, event `/evenimente/{slug}` · `/en/events/{slug}` (same slug in both locales); gallery `/galerie` · `/en/gallery`; contact `/contact` · `/en/contact`; faq `/intrebari-frecvente` · `/en/faq`.

- [ ] **Step 1: Write the failing tests**

```ts
// routes.test.ts
expect(pathFor({ service: 'group' }, 'en')).toBe('/en/what-we-do/group-workshops')
expect(alternatesFor({ event: 'pauza-de-suflet-2' })).toEqual({ ro: '/evenimente/pauza-de-suflet-2', en: '/en/events/pauza-de-suflet-2' })
expect(serviceKeyFromSlug('consiliere', 'ro')).toBe('counselling')
expect(serviceKeyFromSlug('consiliere', 'en')).toBeUndefined()
const ro = allTargets().map(t => pathFor(t, 'ro'))
expect(new Set(ro).size).toBe(ro.length)
for (const p of ro) { expect(p).toMatch(/^\/[a-z0-9\-\/]*$/); expect(p.startsWith('/en')).toBe(false) }
for (const t of allTargets()) expect(pathFor(t, 'en').startsWith('/en')).toBe(true)

// content.test.ts
const strings = (o: unknown): string[] => /* all string leaves */
for (const l of locales) {
  const all = strings(getDictionary(l)).join('\n')
  expect(all).not.toMatch(/[şţŞŢ]/)                      // cedilla forms
  expect(all).not.toMatch(/psiholog|psihoterapeut/i)
  const named = [...Object.values(getDictionary(l).services).map(s => s.name), ...strings(getDictionary(l).meta)].join('\n')
  expect(named).not.toMatch(/terapie|therapy/i)
}
// same shape, same list lengths in both locales
expect(shapeOf(getDictionary('en'))).toEqual(shapeOf(getDictionary('ro')))
// facts are not retyped in copy: prices come from facts
expect(getDictionary('ro').services.counselling.facts.map(f => f.value)).toContain('150 lei / oră')
expect(getDictionary('en').services.private.facts.map(f => f.value).join(' ')).toContain('450 lei')
```

- [ ] **Step 2:** Run both tests → FAIL.
- [ ] **Step 3:** Implement `routes.ts` as two lookup tables (static pages, service slugs) plus the functions above. Write `ro.ts` from `docs/content/ro.md` and `en.ts` from `docs/content/en.md` section by section, typing `en` as `Dictionary`. Prices and the event date are built from `facts` with `formatPrice` (never typed as text). Items marked `⟨ÎN CURÂND⟩` are `null` (single values) or `[]` (lists); the views render `<ComingSoon>` for them. Card lines marked `◇` are kept as written. `meta` titles/descriptions: write one per page from that page's own copy (≤ 60 / ≤ 155 chars).
- [ ] **Step 4:** Run tests → PASS. `npm run typecheck` → no errors (EN shape matches RO).
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 4: Design tokens, fonts and base components

**Files:**
- Create: `src/styles/tokens.css`, `src/styles/globals.css`, `src/lib/fonts.ts`, `src/components/{Section,Button,ComingSoon,Logo}.tsx` (+ `.module.css`)
- Test: `tests/unit/tokens.test.ts`

**Interfaces:**
- Produces:
  - CSS custom properties named exactly as DESIGN.md frontmatter (`--ink`, `--clay-600`, `--umber-900`, `--dusk-fg`, `--dusk-fg-2`, `--dusk-fg-3`, `--dusk-accent`, `--dusk-title`, `--dusk-line`, …), plus `--f-display`, `--f-sans`, `--f-script`, `--ease-out`, `--ease-in-out`, `--wrap`, `--gutter`.
  - `fonts` from `src/lib/fonts.ts`: `display` (Fraunces, `axes: ['opsz']`, `style: ['normal','italic']`, variable `--f-display`), `sans` (Jost, `--f-sans`), `script` (Pinyon_Script, weight `'400'`, `--f-script`), all `subsets: ['latin','latin-ext']`, `display: 'swap'`.
  - `<Section surface: 'dusk' | 'dawn' | 'sand' | 'footer', id?: string, labelledBy?: string, children>`: sets the surface tier (`--fg`, `--fg-2`, `--fg-3`, `--line`, `--bg`) via `data-surface`; `dawn` is the decorative gradient band (`aria-hidden`, no children).
  - `<Button href: string, variant: 'primary' | 'ghost', glow?: boolean, children>`: pill with arrow well for primary; `glow` adds `data-glow`.
  - `<ComingSoon label: string, title: string, text: string>`
  - `<Logo variant: 'lockup' | 'wordmark' | 'symbol', className?: string, title?: string>`: inline SVG with `currentColor`, paths taken from `public/logo/ava-logo-horizontal.svg` / `ava-logo-stacked.svg` / `ava-symbol.svg` (switch their fills/strokes to `currentColor`).

- [ ] **Step 1: Write the failing tests** (`tokens.test.ts`; parse `--name: #hex` pairs from `tokens.css`; WCAG relative-luminance `contrast()` helper inside the test)

```ts
const pairs: [string, string, number][] = [
  ['--ink', '--sand-100', 4.5], ['--ink-soft', '--sand-200', 4.5], ['--muted', '--sand-100', 4.5],
  ['--clay-600', '--sand-200', 4.5], ['--dusk-fg-2', '--umber-700', 4.5], ['--dusk-fg-3', '--umber-700', 4.5],
  ['--dusk-accent', '--umber-900', 4.5], ['--dusk-title', '--umber-900', 4.5],
]
for (const [fg, bg, min] of pairs) expect(contrast(tokens[fg], tokens[bg])).toBeGreaterThanOrEqual(min)
// Surface Tier / Dusk Tier rules: colours live only in tokens.css
for (const file of globSync('src/**/*.css').filter(f => !f.endsWith('tokens.css')))
  expect(readFileSync(file, 'utf8')).not.toMatch(/#[0-9a-f]{3,8}\b/i)
```

- [ ] **Step 2:** Run → FAIL (no tokens yet).
- [ ] **Step 3:** Port tokens and the shared atoms (`.btn`, `.soon`, `.textlink`, selection, focus, scrollbar, `.sr-only`) from `design/directions/index.html`, keeping only direction-B values. Fold the mockup's stray dusk hexes into the tier: `#EADFCD` and `#EFE4D3` → `--dusk-fg-2`, `#F3EADB` → `--dusk-fg`, `#FBE7C4` → `--dusk-accent`, `#FFF7EA` → `--dusk-title`. `--muted` text sits only on `sand-100` or lighter (4.43:1 on `sand-200`); `--dusk-line` is decorative, never the only edge of a control. Keep reduced-motion rules beside each animation.
- [ ] **Step 4:** Run → PASS. `npm run typecheck` → no errors.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 5: Layouts, navigation, language switch, footer

**Files:**
- Create: `src/app/(ro)/layout.tsx`, `src/app/(en)/en/layout.tsx`, `src/components/{SiteNav,MobileMenu,LangSwitch,Footer}.tsx` (+ css), `src/app/(ro)/not-found.tsx`, `src/app/(en)/en/not-found.tsx`, `src/app/(ro)/[...missing]/page.tsx`, `src/app/(en)/en/[...missing]/page.tsx`, `src/views/NotFoundPage.tsx`, temporary `src/app/(ro)/page.tsx` and `src/app/(en)/en/page.tsx` rendering `<h1>` only (Task 7 replaces them)
- Test: `tests/e2e/shell.spec.ts`

**Interfaces:**
- Consumes: `getDictionary`, `pathFor`, `alternatesFor` (Task 3); `fonts`, `Logo`, `Section` (Task 4).
- Produces:
  - `<SiteNav locale: Locale, current: RouteTarget, onDark?: boolean>`: lockup, links to the six top pages (`aria-current` on the current one), `LangSwitch`, menu button under 900px.
  - `<LangSwitch locale: Locale, alternates: Record<Locale, string>>`: two links (`RO`, `EN`), current one `aria-current="true"`; real `<a href>` so it works without JS.
  - `<MobileMenu>` (client): full-screen sheet, focus moves to close button, Escape and link click close it and return focus to the menu button.
  - `<Footer locale>`: contact as plain selectable text, Instagram link, page links (all six), legal links pointing to `#` with the "În curând" tag until M5, PFA line from content (Coming soon).
  - Root layouts set `<html lang>`, font variables, `<Woodsprites />` slot (filled in Task 6), and `metadataBase` from `NEXT_PUBLIC_SITE_URL`.

- [ ] **Step 1: Write the failing e2e tests** (`shell.spec.ts`)

```ts
test('html lang per locale', async ({ page }) => {
  await page.goto('/'); await expect(page.locator('html')).toHaveAttribute('lang', 'ro')
  await page.goto('/en'); await expect(page.locator('html')).toHaveAttribute('lang', 'en')
})
test('language switch keeps the page', async ({ page }) => {
  await page.goto('/ce-facem/ateliere-de-grup')
  await page.getByRole('link', { name: 'EN' }).click()
  await expect(page).toHaveURL('/en/what-we-do/group-workshops')
  await page.goto('/en/events/pauza-de-suflet-2')
  await page.getByRole('link', { name: 'RO' }).click()
  await expect(page).toHaveURL('/evenimente/pauza-de-suflet-2')
})
test('mobile menu opens, Escape closes, focus returns', async ({ page }, info) => {
  test.skip(info.project.name !== 'mobile')
  await page.goto('/')
  const btn = page.getByRole('button', { name: 'Meniu' })
  await btn.click(); await expect(page.getByRole('dialog')).toBeVisible()
  await page.keyboard.press('Escape'); await expect(page.getByRole('dialog')).toBeHidden()
  await expect(btn).toBeFocused()
})
test('unknown URL is a localised 404', async ({ page }) => {
  expect((await page.goto('/nu-exista'))!.status()).toBe(404)
  expect((await page.goto('/en/missing'))!.status()).toBe(404)
  await expect(page.locator('html')).toHaveAttribute('lang', 'en')
})
```

- [ ] **Step 2:** `npm run e2e -- shell.spec.ts` → FAIL (the language-switch test needs the service page from Task 8 and the event page from Task 9 and stays failing until Task 9; everything else must pass here).
- [ ] **Step 3:** Implement layouts and components. The `[...missing]` pages call `notFound()`.
- [ ] **Step 4:** Run → the three non-switch tests PASS.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 6: Woodsprite light

**Files:**
- Create: `src/lib/woodsprites.ts`, `src/components/Woodsprites.tsx`
- Modify: both root layouts (render `<Woodsprites />` once after `<main>`)
- Test: `tests/unit/woodsprites.test.ts`, `tests/e2e/woodsprites.spec.ts`

**Interfaces:**
- Produces:
  - `type Sprite = { x: number; y: number; vx: number; vy: number; hx: number; hy: number; layer: 0 | 1 | 2; phase: number; follower: boolean; k: number; c: number; orbit: number; spin: number; size: number; pulse: number }`
  - `type SpriteInput = { pointer: { x: number; y: number } | null; attract: { x: number; y: number; r: number } | null }`
  - `seedSprites(count: number, width: number, height: number, rand: () => number): Sprite[]` (B values: count 44, follower share .6, layers far/mid/near = scale .45/.75/1.1, alpha .45/.7/1, drift .35/.6/1, stiffness ×.5/.8/1; one in seven on near; stiffness 7–16 /s², damping .72 of critical; orbit 26–146px)
  - `stepSprites(sprites: Sprite[], dt: number, t: number, input: SpriteInput, width: number, height: number): void` (dt clamped to .05)
  - `<Woodsprites />` client canvas: fixed, full viewport, `pointer-events: none`, `aria-hidden`, z-index under nav and menu; additive compositing, alpha .9, size 1.15; pointer idle after 3.5 s stops following; hovering or focusing `[data-glow]` sets `attract` (r = 0.55 × larger side); pauses on `visibilitychange`; DPR cap 2. Sets `data-state` on the canvas to `running` or `still`.

- [ ] **Step 1: Write the failing tests**

```ts
// woodsprites.test.ts — seeded PRNG (mulberry32(42)) passed as rand
const s = seedSprites(44, 1280, 800, rand)
expect(s.filter(p => p.follower).length).toBeGreaterThan(18)
const input = { pointer: { x: 640, y: 400 }, attract: null }
for (let i = 0; i < 180; i++) stepSprites(s, 1 / 60, i / 60, input, 1280, 800)
const meanDist = avg(s.filter(p => p.follower).map(p => Math.hypot(p.x - 640, p.y - 400)))
expect(meanDist).toBeLessThan(170)
for (const p of s.filter(p => !p.follower)) expect(Math.hypot(p.x - p.hx, p.y - p.hy)).toBeLessThan(60)
stepSprites(s, 5, 10, input, 1280, 800)                  // a 5 s frame (tab was asleep)
for (const p of s) expect(Number.isFinite(p.x) && Number.isFinite(p.y)).toBe(true)
```

```ts
// woodsprites.spec.ts
test('reduced motion draws one still frame', async ({ page }) => {
  await page.emulateMedia({ reducedMotion: 'reduce' }); await page.goto('/')
  await expect(page.locator('canvas[data-state]')).toHaveAttribute('data-state', 'still')
})
test('runs normally', async ({ page }) => {
  await page.goto('/'); await expect(page.locator('canvas[data-state]')).toHaveAttribute('data-state', 'running')
})
```

- [ ] **Step 2:** Run both → FAIL.
- [ ] **Step 3:** Port the physics and drawing from the `Sprites` module in `design/directions/index.html` (direction B config, no scroll term) into the pure functions above; the component owns only the canvas, texture, rAF loop and listeners.
- [ ] **Step 4:** Run → PASS.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 7: Home page (direction B)

**Files:**
- Create: `src/views/HomePage.tsx` (+ css), `src/components/{ServiceRail,Steps,EventCard,FaqList,NewsletterForm}.tsx` (+ css)
- Modify: `src/app/(ro)/page.tsx`, `src/app/(en)/en/page.tsx` (render `<HomePage locale>`)
- Test: `tests/e2e/home.spec.ts`

**Interfaces:**
- Consumes: Tasks 2–6. `NewsletterForm` posts to `subscribe` from Task 8 (render the form now, wire in Task 8).
- Produces:
  - `<HomePage locale: Locale>`; both home page files `export const revalidate = 3600` so "next event" follows the calendar
  - `<ServiceRail locale, items: { key: ServiceKey; name: string; line: string; image: string; soon?: boolean }[]>`: horizontal scroll-snap rail, focusable region with label; an item with `soon` shows the "în pregătire" tag (Retreaturi)
  - `<Steps items: string[]>` (ordered list, script numerals)
  - `<EventCard locale, event: EventFacts, copy: EventCopy>`: date panel first (weekday, day, script month, time), title, series, description, facts list (where = `facts.area`, price, with), seats line when `seatsLeft` is a number, primary `Button` "Mă înscriu" → `pathFor({ event: slug })` (M3 replaces the target with checkout), "Toate evenimentele" link
  - `<FaqList items: { q: string; a: string }[]>`: `<details>` per question (works without JS)

Block order (contract FIRST VIEWPORT + `docs/sitemap.md`): hero on `dusk` (photo `hero-dusk-terracotta.webp` via `next/image` `priority`, umber veil, nav `onDark`, wordmark, script tagline, lead, primary "Vezi atelierele" → group service with `glow`, ghost "Pentru companii" → companies service) · about (script heading + lead + "Povestea noastră") · services rail (5 cards: group, companies, counselling, private, retreats with `soon`) · steps · `dawn` band · next event (`nextEvent(facts.events, new Date())`; none → `ComingSoon` with the no-event copy) · testimonials `ComingSoon` · mini gallery `ComingSoon` · home FAQ (3 questions) · newsletter · footer.

- [ ] **Step 1: Write the failing e2e tests**

```ts
// the server renders with the real clock, so assert the state today's date implies
test('home RO shows the next event or an honest placeholder', async ({ page }) => {
  await page.goto('/')
  const main = page.getByRole('main')
  await expect(page.getByRole('heading', { level: 1 })).toContainText('AVA Art & Soul')
  await expect(main.getByText('în pregătire')).toBeVisible()            // Retreaturi tag in the rail
  if (nextEvent(facts.events, new Date())) {
    await expect(main.getByText('200 lei').first()).toBeVisible()
    await expect(main.getByRole('link', { name: /Mă înscriu/ })).toHaveAttribute('href', '/evenimente/pauza-de-suflet-2')
    await expect(main.getByText('În curând')).toHaveCount(2)            // testimonials + gallery
  } else {
    await expect(main.getByRole('link', { name: /Mă înscriu/ })).toHaveCount(0)
    await expect(main.getByText('În curând')).toHaveCount(3)            // + next event in preparation
  }
})
test('two doors in the first viewport', async ({ page }) => {
  await page.goto('/')
  await expect(page.getByRole('link', { name: 'Vezi atelierele' })).toBeInViewport()
  await expect(page.getByRole('link', { name: 'Pentru companii' }).first()).toBeInViewport()
})
test('home EN', async ({ page }) => {
  await page.goto('/en'); await expect(page.getByRole('link', { name: 'See the workshops' })).toHaveAttribute('href', '/en/what-we-do/group-workshops')
})
```

- [ ] **Step 2:** Run → FAIL.
- [ ] **Step 3:** Build the view from the mockup's `.dir-b` markup and CSS, using `Section` surfaces and the `--dusk-*` tokens; entrance animation once on the hero (`[data-enter]` rise, 70 ms stagger), scroll reveal only via `animation-timeline: view()` inside `@supports`.
- [ ] **Step 4:** Run → PASS on both projects.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 8: Service pages, forms and contact

**Files:**
- Create: `src/views/{ServicesPage,ServicePage,ContactPage}.tsx` (+ css), `src/app/(ro)/ce-facem/page.tsx`, `src/app/(ro)/ce-facem/[service]/page.tsx`, `src/app/(en)/en/what-we-do/page.tsx`, `src/app/(en)/en/what-we-do/[service]/page.tsx`, `src/app/(ro)/contact/page.tsx`, `src/app/(en)/en/contact/page.tsx`, `src/lib/forms.ts`, `src/actions/forms.ts`, `src/components/ContactForm.tsx`
- Modify: `src/components/NewsletterForm.tsx` (wire to `subscribe`)
- Test: `tests/unit/forms.test.ts`, `tests/e2e/services.spec.ts`

**Interfaces:**
- Consumes: Tasks 2–7.
- Produces:
  - `generateStaticParams` for the six services per locale; unknown slug → `notFound()`.
  - `<ServicePage locale, service: ServiceKey>` in the sitemap template order: for whom · what happens · what you get · who facilitates · facts block (duration / price / place) · testimonials (`ComingSoon`) · FAQ (`FaqList`) · CTA (`Button`; sticky bar on mobile). Retreats renders `ComingSoon` for programme, inclusions, price and its three unknown FAQ answers.
  - `type ContactInput = { name: string; email: string; phone?: string; interest: 'group' | 'companies' | 'counselling' | 'private' | 'retreat' | 'collaboration' | 'other'; message: string; gdpr: true }`
  - `type FieldErrors = Partial<Record<'name' | 'email' | 'phone' | 'interest' | 'message' | 'gdpr', 'required' | 'invalid' | 'tooLong'>>`
  - `validateContact(data: FormData): { ok: true; value: ContactInput } | { ok: false; errors: FieldErrors }` (name ≤ 120, message ≤ 4000, phone optional `^[+0-9 ()-]{6,20}$`, email `^[^\s@]+@[^\s@]+\.[^\s@]{2,}$`, gdpr must be `'on'`)
  - `validateEmail(value: unknown): boolean`
  - Server actions `subscribe(prev, formData)` and `sendContact(prev, formData)` → `{ status: 'invalid'; errors: FieldErrors } | { status: 'unavailable' } | { status: 'sent' }`. Until M4 a valid submission returns `unavailable` when `BREVO_API_KEY` is unset; the UI then shows the forms copy "Formularul nu e încă activ. Scrie-ne la ava.events.26@gmail.com." Messages render as text, never HTML.

- [ ] **Step 1: Write the failing tests**

```ts
// forms.test.ts
const fd = (o: Record<string, string>) => { const f = new FormData(); for (const [k, v] of Object.entries(o)) f.set(k, v); return f }
const good = { name: 'Ana', email: 'ana@exemplu.ro', interest: 'group', message: 'Salut', gdpr: 'on' }
expect(validateContact(fd(good)).ok).toBe(true)
expect(validateContact(fd({ ...good, gdpr: '' }))).toEqual({ ok: false, errors: { gdpr: 'required' } })
expect(validateContact(fd({ ...good, email: 'ana@' }))).toEqual({ ok: false, errors: { email: 'invalid' } })
expect(validateContact(fd({ ...good, message: 'x'.repeat(10_000) }))).toEqual({ ok: false, errors: { message: 'tooLong' } })
expect(validateContact(fd({ ...good, interest: 'hack' }))).toEqual({ ok: false, errors: { interest: 'invalid' } })
expect(validateContact(fd({ ...good, name: '  ' }))).toEqual({ ok: false, errors: { name: 'required' } })
expect(validateEmail('nume@exemplu.ro')).toBe(true); expect(validateEmail(42)).toBe(false)
```

```ts
// services.spec.ts
for (const [path, price] of [['/ce-facem/consiliere', '150 lei / oră'], ['/ce-facem/atelier-privat', '450 lei'], ['/en/what-we-do/group-workshops', '185 lei']])
  test(`price on ${path}`, async ({ page }) => { await page.goto(path); await expect(page.getByText(price).first()).toBeVisible() })
test('unknown service is 404', async ({ page }) => { expect((await page.goto('/ce-facem/nimic'))!.status()).toBe(404) })
test('contact form shows field errors without echoing HTML', async ({ page }) => {
  await page.goto('/contact')
  await page.getByLabel('Nume').fill('<img src=x onerror=alert(1)>')
  await page.getByRole('button', { name: /Trimite/ }).click()
  await expect(page.locator('img[src="x"]')).toHaveCount(0)
  await expect(page.getByText(/acordul/i)).toBeVisible()               // gdpr required message
})
```

- [ ] **Step 2:** Run → FAIL.
- [ ] **Step 3:** Implement. Forms use `useActionState`, native `required`/`type="email"`, labels on every field, `aria-invalid` + `aria-describedby` on errors, inputs at 16px font size.
- [ ] **Step 4:** Run unit + e2e → PASS.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 9: About, events, gallery, FAQ; SEO

**Files:**
- Create: `src/views/{AboutPage,EventsPage,EventPage,GalleryPage,FaqPage}.tsx` (+ css) and their page files in both groups (`despre-noi`, `evenimente`, `evenimente/[slug]`, `galerie`, `intrebari-frecvente` · `about`, `events`, `events/[slug]`, `gallery`, `faq`), `src/lib/seo.ts`, `src/lib/jsonld.ts`, `src/components/JsonLd.tsx`, `src/app/sitemap.ts`, `src/app/robots.ts`
- Modify: every page file (export `generateMetadata` via `buildMetadata`), `tests/e2e/smoke.spec.ts` (remove the fixme)
- Test: `tests/unit/seo.test.ts`, `tests/e2e/pages.spec.ts`

**Interfaces:**
- Consumes: everything above.
- Produces:
  - `buildMetadata(target: RouteTarget, locale: Locale): Metadata`: title `{meta.title} — AVA Art & Soul` (home: `AVA Art & Soul — {tagline}`), description, `alternates.canonical`, `alternates.languages` `{ 'ro-RO': ro, en: en, 'x-default': ro }` (absolute URLs), Open Graph (`ro_RO` / `en_GB`, hero image)
  - `organizationLd()`, `faqPageLd(items)`, `eventLd(event: EventFacts, copy: EventCopy, locale)`, `personLd(locale)` (Alessia, `jobTitle` = "Consilier în dezvoltare personală" / "Personal-development counsellor"), `breadcrumbLd(items)`; `<JsonLd data>` renders `<script type="application/ld+json">`
  - About: story, Alessia (photo `ComingSoon`), training list, team cards with `public/img/team/` photos (Iuliana Petrescu, Casandra Samargiu), values `ComingSoon`. Events: upcoming list via `nextEvent` ordering, archive `ComingSoon`; event detail with `EventCard`, past events (start ≤ now) show "a avut loc" / "took place" and no booking button. Events list and event detail pages `export const revalidate = 3600`. Gallery: three category `ComingSoon` cards + Instagram link. FAQ: general list.

- [ ] **Step 1: Write the failing tests**

```ts
// seo.test.ts (NEXT_PUBLIC_SITE_URL='https://example.test')
const m = buildMetadata({ service: 'counselling' }, 'en')
expect(m.alternates?.canonical).toBe('https://example.test/en/what-we-do/counselling')
expect(m.alternates?.languages).toEqual({ 'ro-RO': 'https://example.test/ce-facem/consiliere', en: 'https://example.test/en/what-we-do/counselling', 'x-default': 'https://example.test/ce-facem/consiliere' })
const copy = getDictionary('ro').events['pauza-de-suflet-2']
const e = eventLd(facts.events[0], copy, 'ro')
expect(e.startDate).toBe('2026-11-15T18:00:00+02:00')
expect(e.offers).toMatchObject({ price: '200', priceCurrency: 'RON', availability: 'https://schema.org/InStock' })
expect(eventLd({ ...facts.events[0], seatsLeft: 0 }, copy, 'ro').offers.availability).toBe('https://schema.org/SoldOut')
expect(JSON.stringify(personLd('ro'))).not.toMatch(/psiholog|terapeut/i)
```

```ts
// pages.spec.ts — every target, both locales
for (const path of ALL_PATHS) test(`${path} renders`, async ({ page }) => {
  const res = await page.goto(path); expect(res!.status()).toBe(200)
  await expect(page.locator('h1')).toHaveCount(1)
  await expect(page.locator('link[rel="alternate"][hreflang="x-default"]')).toHaveCount(1)
})
test('sitemap lists both locales', async ({ request }) => {
  const xml = await (await request.get('/sitemap.xml')).text()
  expect(xml).toContain('/ce-facem/consiliere'); expect(xml).toContain('/en/what-we-do/counselling')
})
```
(`ALL_PATHS` = `allTargets()` × `locales` through `pathFor`, imported from `src/i18n/routes.ts`.)

- [ ] **Step 2:** Run → FAIL.
- [ ] **Step 3:** Implement. `sitemap.ts` emits every target with `alternates.languages`; `robots.ts` allows all and points to the sitemap.
- [ ] **Step 4:** Run unit + e2e → PASS, including `smoke.spec.ts` and the language-switch test from Task 5.
- [ ] **Step 5: Checkpoint.** Do not commit.

---

### Task 10: Whole-site checks and finish review

**Files:**
- Test: `tests/e2e/quality.spec.ts`
- Modify: whatever the checks find

- [ ] **Step 1: Write the tests**

```ts
for (const width of [320, 375]) for (const path of ALL_PATHS)
  test(`${path} no horizontal scroll at ${width}`, async ({ page }) => {
    await page.setViewportSize({ width, height: 800 }); await page.goto(path)
    expect(await page.evaluate(() => document.documentElement.scrollWidth)).toBeLessThanOrEqual(width)
  })
test.describe('without JavaScript', () => {
  test.use({ javaScriptEnabled: false })
  test('home content and footer links are visible', async ({ page }) => {
    await page.goto('/')
    await expect(page.getByRole('heading', { level: 1 })).toBeVisible()
    await expect(page.getByRole('contentinfo').getByRole('link', { name: 'Ce facem' })).toBeVisible()
    for (const el of await page.locator('main h2, main p').all()) expect(await el.evaluate(n => getComputedStyle(n).opacity)).not.toBe('0')
  })
})
test('fonts render Romanian diacritics', async ({ page }) => {
  await page.goto('/'); await page.evaluate(() => document.fonts.ready)
  for (const v of ['--f-display', '--f-sans', '--f-script'])   // next/font hashes family names: read them from the variables
    expect(await page.evaluate(name => document.fonts.check(`16px ${getComputedStyle(document.body).getPropertyValue(name)}`, 'șțȘȚăîâ'), v)).toBe(true)
})
```

- [ ] **Step 2:** Run `npm test && npm run typecheck && npm run e2e` → fix every failure, rerun until all pass.
- [ ] **Step 3:** Run `"<impeccable>/scripts/impeccable" detect --json src` once; fix mechanical findings.
- [ ] **Step 4:** Capture `.impeccable/review/desktop.png` (1440 wide, full page) and `mobile.png` (390 wide) of `/`, then spawn `impeccable:impeccable-finish-reviewer` with the request, the contract (`.impeccable/surfaces/src-views-homepage-tsx.md`), the screenshots, the detector output, `design/directions/index.html` (direction B) as the critique reference and `reference/craft-floor.md`. Act on its disposition (max two fix rounds).
- [ ] **Step 5:** Run `superpowers:verification-before-completion`: paste the final `npm test`, `npm run typecheck`, `npm run e2e` and `npm run build` outputs.
- [ ] **Step 6: Checkpoint.** `git status`; summarise the changed files for the user. Do not commit.
