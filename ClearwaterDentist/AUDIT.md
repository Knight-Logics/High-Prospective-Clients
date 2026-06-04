# Clearwater Dentist — Digital Presence Audit

**Client:** Dr. Nadia Pokrovskaya, D.M.D. — Clearwater Dentist  
**Domain:** https://www.clearwaterdentist.com/  
**Audit date:** June 4, 2026  
**Prepared for:** Office visit + custom rebuild + CRM/automation discovery  
**Address:** 1700 N McMullen Booth Rd, Ste A1, Clearwater, FL 33759  
**Agency:** Xpress, INC (Duda platform)  

**Decision:** ✅ **Custom rebuild confirmed** — replica in progress at `rebuild/` (72 pages, 441 assets)

---

## Executive summary

Clearwater Dentist has **real competitive assets**: exact-match domain, compelling doctor story, anxiety-free positioning, therapy dogs, emergency dentistry, implants, cosmetic services, facial esthetics, financing, videos, reviews, and an **active 2026 blog**. Dr. Nadia showed strong interest in a **CRM / automation system** — clarify pricing as **$1,500 setup + ~$400/mo** (not $1,500/mo).

The biggest problems are **conversion confusion** (6+ phone numbers, two booking systems), **duplicate/placeholder content**, **mobile performance** (LCP 9.4s), **Duda runtime errors**, and **vendor lock-in** through Xpress on Duda — not WordPress.

| Area | Grade | One-line verdict |
|------|-------|------------------|
| Brand & positioning | B+ | Strong boutique/anxiety-free angle; messaging scattered |
| Conversion flow | **D** | Multiple phones, booking paths, repeated CTAs |
| SEO foundation | B- | Good coverage + blog; structure needs cleanup |
| Local SEO | B- | Exact-match domain; NAP inconsistency visible |
| Content quality | C+ | Duplicates, placeholders, empty financing pages |
| Technical / UX | C | Duda bloat; ChunkLoadErrors; 49/90 resources fail in Google test |
| Structured data | B- | 7 valid items; 3 redundant Dentist blocks |
| Performance (mobile) | **D+** | PSI **66** — LCP **9.4s** |
| Performance (desktop) | B | PSI **89** |
| CRM / automation readiness | **?** | Primary client interest — systems discovery needed |
| Compliance / HIPAA | B-/C+ | Privacy policy exists; vendor BAAs unverified |

---

## Client meeting notes (Jun 4, 2026)

| Topic | Detail |
|-------|--------|
| **Primary interest** | CRM system + automation (not just website) |
| **Pricing confusion** | You quoted **$1,500** — she heard **$1,500/month** |
| **Recommended clarify** | **$1,500 upfront** (setup/rebuild/CRM config) + **~$400/month** ongoing (hosting, CRM seats, automation maintenance, optional SEO/content) |
| **Platform assumption** | Site is **Duda**, not WordPress — custom rebuild is correct path |
| **Rebuild status** | Full 72-page replica building in `rebuild/` — preview at `http://localhost:3457` |

### Suggested pricing talk track

> "The $1,500 is a one-time setup — that covers the custom website rebuild, CRM wiring, form automations, and getting your phones and booking consistent. Ongoing would be around $400 a month for hosting, CRM, and keeping automations running — not fifteen hundred a month."

---

## Critical discovery: NOT WordPress — Duda + Xpress

| Signal | Finding |
|--------|---------|
| HTML `SiteType` | **DUDAONE** (Duda website builder) |
| CDN | `irp.cdn-website.com/a227a250` |
| Footer | "Website designed and maintained by **Xpress, INC**" |
| Server | nginx (Duda hosting) |

**Implication:** Cannot "customize WordPress." Custom rebuild on static/modern stack is the right deliverable. Ask what they pay Xpress monthly and whether they own content for migration.

---

## PageSpeed Insights (Jun 3, 2026)

Sources: [Mobile PSI](https://pagespeed.web.dev/analysis/https-www-clearwaterdentist-com/6zlhhreqp8?form_factor=mobile) · [Desktop PSI](https://pagespeed.web.dev/analysis/https-www-clearwaterdentist-com/6zlhhreqp8?form_factor=desktop)

**No CrUX field data** — insufficient real-user traffic in Chrome UX Report.

| Metric | Mobile | Desktop |
|--------|--------|---------|
| **Performance** | **66** 🟠 | **89** 🟠 |
| Accessibility | 93 🟢 | 93 🟢 |
| Best Practices | 77 🟠 | 73 🟠 |
| SEO (Lighthouse) | 92 🟢 | 92 🟢 |
| FCP | 3.9s 🔴 | 0.8s 🟢 |
| **LCP** | **9.4s** 🔴 | 1.3s 🟠 |
| TBT | 50ms 🟢 | 210ms 🟠 |
| CLS | 0.019 🟢 | 0 🟢 |
| Speed Index | 3.9s 🟠 | 0.8s 🟢 |

**Mobile filmstrip:** ~4 blank white frames before content — patients bounce before seeing CTAs.

**Top Lighthouse opportunities (mobile):**
1. Render-blocking requests (~300ms)
2. Efficient cache lifetimes (~19 KiB)
3. Network dependency tree
4. Font display (~10ms)
5. Image delivery (~14 KiB)

**Rebuild target:** Mobile LCP **< 2.5s**, Performance **90+**.

---

## Structured data & Rich Results Test

Source: [Rich Results Test — Jun 3, 2026](https://search.google.com/test/rich-results/result?id=Izy7JEPzZrgP0xQMRVBSeQ)

| Detected | Status |
|----------|--------|
| Local businesses (Dentist) | ✅ 3 valid — non-critical warnings (`priceRange`, `image` missing on one block) |
| Organization | ✅ 3 valid |
| Review snippets | ✅ 1 valid |

**Crawl:** Successful · Jun 3, 2026 10:32:15 PM · Google Inspection Tool smartphone

### Schema issues

- **Three separate Dentist blocks** — redundant (Duda auto + manual)
- One block uses **page SEO title** as schema `name` instead of "Clearwater Dentist"
- No `Physician` entity for Dr. Nadia Pokrovskaya, D.M.D.
- Missing `openingHours`, canonical `telephone` in some blocks
- Missing `priceRange` (optional warning)

Exported: `schema-current.json` · Rebuild consolidates to one Dentist + Physician.

---

## JavaScript errors & Duda runtime failures

Rich Results "Tested page" console (critical for pitch):

| Error | Impact |
|-------|--------|
| `Uncaught SyntaxError: '#1300582767' is not a valid selector` | Broken DOM query on homepage |
| **ChunkLoadError** ×6 — Duda runtime chunks fail to load | Layout modules, anchors, mobile runtime break |
| `Init initAnchorsApp failed` | In-page anchor navigation broken |
| CORS errors on Google Ads conversion pixels | Tracking may be unreliable |
| **49/90 page resources couldn't load** in Google's test | Images, fonts, Duda JS chunks |

**Google Ads call tracking snippet** references **`7277580243`** in conversion URL — another phone inconsistency source.

**Third-party scripts detected:**
- Google Tag Manager / GA4 (`G-70P2GLMWC7`)
- Google Ads conversion (`17534174030`)
- Duda analytics (`d32hwlnfiv2gyn.cloudfront.net`)
- Dentrix Ascend booking links
- GetWeave booking (homepage)
- Embedded Google Maps

**Risk:** Bloated Duda runtime + broken chunks + overlapping tracking = poor mobile UX and unreliable attribution. Custom rebuild eliminates ChunkLoadErrors entirely.

---

## Pros (what's working)

### Domain & brand
- **ClearwaterDentist.com** — premium exact-match local domain
- Differentiators: boutique one-patient-at-a-time, Dr. Nadia's surgical/implant/sedation background, therapy dogs, same-day emergency, facial esthetics
- Doctor narrative: Tufts D.M.D., Harvard post-bacc, Air Force oral surgery training, 27+ years

### Content & services
- **72 URLs** in sitemap — broad service coverage
- Active blog with 2026 posts (March–June)
- Before/after gallery, patient videos, financing hub, real embedded reviews

### SEO & accessibility
- Lighthouse SEO **92** · Accessibility **93**
- Rich Results: 7 valid items
- Clean robots.txt + XML sitemap
- Most service pages have unique titles and meta descriptions

---

## Cons (risks & opportunities)

### 🚨 P0: Multiple phone numbers

| Number | Where |
|--------|-------|
| **(727) 797-8444** | Header |
| **(727) 285-8132** | Footer, Book Online CTAs |
| **(727) 758-0243** | Homepage Call Now + **Google Ads conversion snippet** |
| 727-591-4577, 727-610-7702, 727-300-0253 | Footer — unexplained |

### 🚨 P0: Dual booking systems

| System | Pages |
|--------|-------|
| **Dentrix Ascend** | 70/72 |
| **GetWeave** | Homepage + therapy dog page |

### Homepage trust issues
- Duplicate "Welcome to Clearwater Dentist" + "Individualized Care" sections
- **4 H1 tags** on homepage
- Placeholder gallery: "Nature's Symphony", "Faces of Humanity", "Beyond Boundaries"
- Claims **24/7 emergency** but hours are Mon–Fri 9–5

### Empty / weak pages
- `/alphaeon` — title "Alphaeon", no H1, empty body
- `/sunbit` — no H1
- 10+ blog/article pages missing H1

---

## Screaming Frog / sitemap crawl (Jun 4, 2026)

**72 URLs** crawled · **0 internal 4xx** · Exports: `crawl-screaming-frog/`

| Finding | Detail |
|---------|--------|
| Internal HTML URLs | 72 |
| 4xx errors | 0 |
| Missing H1 | 10+ pages |
| Multiple H1 | Homepage (4) |
| Phone variants sitewide | 6+ |
| Thin pages (<300 words) | 0 (Duda template bloat — 2,600+ words/page) |

Screaming Frog CLI blocked (licence file missing). See `crawl-screaming-frog/CRAWL-SUMMARY.md`.

---

## Technical scan summary

```
Host:           www.clearwaterdentist.com
Platform:       Duda (DUDAONE) — NOT WordPress
Agency:         Xpress, INC
CDN:            irp/lirp/static/vid.cdn-website.com
Site alias:     a227a250
Server:         nginx
Homepage HTML:  ~73 KB (gzip)
JSON-LD:        Yes — 3× Dentist + Organization + Review
Booking:        Dentrix Ascend + GetWeave
Analytics:      GA4 G-70P2GLMWC7 + Google Ads
robots.txt:     ✅ Sitemap declared
SSL:            ✅ HSTS enabled
Cache-Control:  no-cache, must-revalidate (poor caching)
```

---

## CRM & automation opportunities (client's primary interest)

**Goal at visit:** Map manual workflows → recommend CRM + automations.

### Likely CRM / automation stack for dental

| Function | Options to discover |
|----------|---------------------|
| CRM / patient comms | Weave (already linked), HubSpot, GoHighLevel, Dentrix-native |
| Booking | Dentrix Ascend (primary) |
| Review requests | Weave, Birdeye, manual |
| Missed-call text-back | Weave, CallRail, custom |
| Form → CRM | Currently unknown destination |
| Email nurture | Unknown — may be none |
| SMS reminders | Privacy policy mentions SMS — verify vendor |

### Automation quick wins (post-rebuild)

1. **Single phone + single booking URL** everywhere — including Ads conversion tracking
2. **Form submit → CRM** — instant SMS/email to coordinator + patient auto-reply
3. **Missed call → SMS** — "Sorry we missed you — book online or call back"
4. **Review request sequence** — 24h post-visit → Google review link
5. **New patient nurture** — welcome email + financing info + anxiety FAQ
6. **Emergency funnel** — dedicated landing + click-to-call tracking
7. **Monthly dashboard** — calls, form submits, bookings, ad spend

### Questions for systems discovery

- What happens when contact form submits?
- Who manages Google Ads? Monthly spend?
- Dentrix Ascend admin — who has access?
- Is Weave active CRM or leftover link?
- EMR/PMS beyond Dentrix?
- Who answers phone, DMs, reviews?
- HIPAA BAAs with Duda, Xpress, form handler, SMS, analytics?

---

## Custom rebuild — status & scope

**Location:** `rebuild/`  
**Preview:** `npm run serve` → http://localhost:3457

| Item | Status |
|------|--------|
| Pages built | ✅ 72/72 |
| Assets downloaded | ✅ 441 (9 failed — videos/fonts 403) |
| Shared header/footer | ✅ From `.dmHeader` / `.dmFooter` |
| Inline Duda CSS preserved | ✅ Per-page styles in `<style>` |
| Fonts | ✅ Be Vietnam, Epilogue, Fjalla One, Poppins, etc. |
| Hero slider | ✅ flexslider auto-rotate |
| Scroll animations | ✅ fadeInUp reveal |
| Mobile nav | ✅ Hamburger drawer |
| Schema | ✅ Consolidated Dentist + Physician |
| Screenshot diff | Run `npm run screenshot` |

### Rebuild fixes baked in (vs live)
- No Duda ChunkLoadErrors
- No broken `#1300582767` selector
- Consolidated schema
- Tracking hooks for phone + booking
- Ready for single canonical phone once confirmed

### Still to polish for 100% visual parity
- Per-page inline CSS from each page (currently homepage styles shared — may need page-specific style extraction)
- Failed video assets (403) — may need client-provided files
- Fine-tune mobile nav to match Duda hamburger exactly
- Side-by-side screenshot QA on all key money pages

---

## 5-phase improvement plan

| Phase | Focus | Investment |
|-------|--------|------------|
| **1 — Rebuild + consistency** | Custom site live, one phone, one booking, remove placeholders | **$1,500 upfront** |
| **2 — CRM + automation** | Form routing, missed-call SMS, review requests, nurture sequences | Included in setup + **~$400/mo** |
| **3 — SEO upgrade** | Schema cleanup, local pages, blog internal links, FAQ schema | Month 2–3 |
| **4 — Performance proof** | Mobile LCP < 2.5s, conversion tracking, Ads alignment | Ongoing |
| **5 — Content polish** | Replace placeholder gallery, fix Alphaeon/Sunbit, E-E-A-T author markup | Month 2–4 |

---

## Pricing guidance (updated)

| Offer | Price | Notes |
|-------|-------|-------|
| **Setup (rebuild + CRM config)** | **$1,500 one-time** | Clarify NOT monthly |
| **Ongoing (hosting + CRM + automation)** | **~$400/month** | Adjust based on CRM seats/tools |
| SEO/content add-on | +$500–$1,500/mo | Optional |
| Duda cleanup only (if they stay) | $750–$1,500 | Not recommended — caps performance |

---

## Priority recommendations (ranked)

### P0 — Revenue & trust
1. Clarify **$1,500 setup vs $400/mo** pricing
2. Confirm **one canonical phone** — align GBP, site, Ads
3. **Single booking path** — Dentrix Ascend
4. Deploy custom rebuild
5. Remove placeholder gallery + duplicate homepage blocks

### P1 — CRM & automation (30 days)
6. Map form → CRM pipeline
7. Missed-call SMS + review automation
8. Conversion tracking (phone, booking, emergency CTA)
9. HIPAA review on form + SMS vendors

### P2 — SEO & growth (60–90 days)
10. Consolidate schema · Physician entity · FAQ schema
11. 3–5 quality nearby-city landing pages
12. Blog → money page internal linking
13. Fix missing H1s on blog/financing pages

---

## Links & evidence

- Website: https://www.clearwaterdentist.com/
- PageSpeed Mobile: https://pagespeed.web.dev/analysis/https-www-clearwaterdentist-com/6zlhhreqp8?form_factor=mobile
- PageSpeed Desktop: https://pagespeed.web.dev/analysis/https-www-clearwaterdentist-com/6zlhhreqp8?form_factor=desktop
- Rich Results: https://search.google.com/test/rich-results/result?id=Izy7JEPzZrgP0xQMRVBSeQ
- Rebuild preview: http://localhost:3457 (after `npm run serve`)

---

## Source files

| File | Contents |
|------|----------|
| `MEETING-PREP.md` | Agenda, CRM checklist, pricing script |
| `PRE-VISIT-AUDITS.md` | Technical pre-visit summary |
| `schema-current.json` | Structured data export |
| `crawl-screaming-frog/` | 72-URL crawl |
| `rebuild/` | Full site replica (72 pages) |

---

*Next: `MEETING-PREP.md` — CRM discovery + pricing clarification.*
