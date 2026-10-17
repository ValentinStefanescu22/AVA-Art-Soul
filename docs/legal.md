# Legal checklist (Romania)

> Not legal advice. Final wording must be checked by the client's accountant or a lawyer before launch.

## Required before taking payments
- [ ] **Business identification in the footer** (Legea 365/2002 privind comerțul electronic): PFA name, CUI, Registrul Comerțului number, registered office, email. ⟨Client to provide⟩
- [ ] **Termeni și condiții**: services, prices in RON with VAT status, how booking and payment work, cancellation, liability, complaints. Required once the site sells directly.
- [ ] **Înscrieri, plată și anulare** (plain-language page): seat confirmed only after full advance payment; no refunds; at least 24 h notice moves the seat to the next workshop. Retreats: separate rules (deposit, deadlines) ⟨Client to define⟩.
- [ ] **Right of withdrawal**: OUG 34/2014 has an exception from the 14-day withdrawal right for leisure services provided on a specific date (art. 16 lit. l). It supports the policy above for dated workshops/events. Vouchers and 1:1 sessions booked for a later date need their own wording. Verify with accountant/lawyer.
- [ ] **ANPC** links in the footer: SAL (soluționarea alternativă a litigiilor) and the EU ODR/SOL platform.
- [ ] Checkout: checkbox "Am citit și accept Termenii și Politica de anulare" before Stripe.

## Privacy (GDPR)
- [ ] **Politica de confidențialitate**: what data each form collects (contact, quote, booking, newsletter, counselling), why, legal basis, retention, processors (Vercel, Stripe, Cal.com, Brevo, Sanity, Google if used), data subject rights, contact.
- [ ] Counselling: collect the minimum; no health details in web forms; state confidentiality.
- [ ] Newsletter: double opt-in (Brevo), unsubscribe in every email; discount pop-up must not pre-tick consent.
- [ ] Photo consent checkbox in the booking form (for gallery use); separate, optional, unticked.
- [ ] Testimonials published only with written consent and chosen display name.

## Cookies
- [ ] **Politica de cookies**. If only cookieless analytics (Vercel Web Analytics) and strictly necessary cookies are used, no consent banner is needed for analytics. Adding Google Analytics / Meta pixel requires a consent banner with "Refuz" as easy as "Accept".

## Wording rules (Colegiul Psihologilor)
Until the founder is registered with the Colegiul Psihologilor, the site never says "psiholog", "psihoterapeut", or offers "terapie" / "art-terapie" as a service. Services are "consiliere în dezvoltare personală" and "autocunoaștere prin artă". Studying experiential therapies and art therapy may be mentioned as education.
