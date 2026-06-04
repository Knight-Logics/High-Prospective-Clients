# Art Form Plastic Surgery — Digital Presence Audit

**Client:** Dr. Christopher Kieliszak ("Dr. K") — Art Form Plastic Surgery  
**Domain:** https://artformplasticsurgery.com/  
**Audit date:** June 3, 2026  
**Prepared for:** Chamber of Commerce follow-up + office visit (systems & automation)  
**Lead contact:** (813) 563-3735 · info@artformplasticsurgery.com  

**Locations:** 801 2nd St N, Safety Harbor, FL 34695 · 1000 W Kennedy Blvd #202, Tampa, FL 33606  

**Knight Logics — source repository (audit, meeting prep, rebuild):**  
https://github.com/Knight-Logics/High-Prospective-Clients/tree/master/Art-Form-Plastic-Surgery  

**Organization:** [Knight-Logics](https://github.com/Knight-Logics) · **Repo:** [High-Prospective-Clients](https://github.com/Knight-Logics/High-Prospective-Clients) (same monorepo as Clearwater Dentist)  

**Local rebuild preview:** `cd rebuild` → `npm install` → `npm run build:fast` → `npm run serve` → http://localhost:3456  

---

## Executive summary

Art Form Plastic Surgery has a **polished brand and strong local reputation** (5.0★ / 102+ Google reviews, active GBP, paid search, sitelinks in organic). The site **looks premium** and is clearly built on **WordPress + Elementor** with professional design.

The biggest gaps are **technical performance on mobile** (critical for patients searching on phones), **thin structured data** for a medical practice, **marketing stack sprawl** (many plugins/scripts), and **missed automation** across booking, reviews, and social. Tomorrow’s visit should focus on **what systems they already pay for** vs. what can be unified.

| Area | Grade | One-line verdict |
|------|-------|------------------|
| Brand & design | A | High-end, trustworthy aesthetic |
| Local SEO (GBP) | A- | Strong reviews; limited social links on profile |
| Organic SEO | B | Sitelinks + indexing good; titles/schema weak |
| Paid search | B- | Running ads; favicon/URL consistency issues |
| Site performance (mobile) | D | PSI 42 — LCP 26.5s is a conversion killer |
| Site performance (desktop) | C+ | PSI 70 — fixable with caching/CSS defer |
| Structured data | C- | Only breadcrumbs validate for rich results |
| Accessibility | C+ | PSI 78 mobile / 74 desktop |
| Social | B- | IG solid; TikTok high effort, low reach |
| Automation readiness | ? | Omnisend, forms, chat, popups — needs discovery |

---

## Pros (what’s working)

### Google Business Profile & local trust
- **5.0 rating** with **102+ reviews** — exceptional for plastic surgery.
- Clear categories, hours, phone, address, photos, and “From the business” copy.
- Two locations (Safety Harbor + Tampa) align with site footer and ad geo targeting.

### Organic search presence
- Branded query shows **sitelinks**: Meet Dr Kieliszak, Book Consultation, About, Gallery, Services — signals site structure Google trusts.
- **Custom favicon** appears on organic results (circular gold profile mark).
- Phone number surfaces in sitelink snippets — good for mobile callers.

### Website brand & content
- Hero messaging (“Unlock Your Natural Radiance…”) is clear and on-brand.
- Service taxonomy is logical: Cosmetic, Reconstructive/Functional, Non-Surgical, Hair, Skincare.
- Strong **patient testimonials** with procedure labels (Rhinoplasty, Botox, etc.).
- Dual CTAs: Book Consultation + click-to-call.
- **Payment Plans** page (Cherry financing mentioned in ads) — reduces price objection.
- Blog present — foundation for long-tail SEO (needs consistency audit).

### Technical foundations (partial)
- **HTTPS** valid (cert expires **July 18, 2026** — renew before lapse).
- **www → non-www** redirect works (canonical host: `artformplasticsurgery.com`).
- **LiteSpeed cache** on Hostinger (`X-LiteSpeed-Cache: hit`) — good host choice.
- **robots.txt** allows crawling; sitemap declared.
- **Google Site Kit** + **Google site verification** TXT present.
- Email on **Google Workspace** (MX → SMTP.GOOGLE.com); SPF includes Google + Mailgun.

### Social — Instagram
- Handle: [@faceplasticsurgeon](https://www.instagram.com/faceplasticsurgeon/)
- **936 followers**, **336 posts** — consistent, professional feed for a local surgeon.
- Bio aligns with practice positioning.

### Advertising
- Active **Google Ads** for high-intent terms (Safety Harbor & Tampa).
- Ad copy highlights board certification, gallery, services, Cherry financing.
- Landing path targets consultation funnel (not just homepage).

---

## Cons (risks & opportunities)

### Critical: mobile performance (PageSpeed Insights)

Source: [PageSpeed Insights — Jun 3, 2026](https://pagespeed.web.dev/analysis/https-artformplasticsurgery-com/3c8pk00hbx?form_factor=desktop)

| Metric | Mobile | Desktop |
|--------|--------|---------|
| **Performance** | **42** 🔴 | **70** 🟠 |
| Accessibility | 78 🟠 | 74 🟠 |
| Best Practices | 96 🟢 | 96 🟢 |
| SEO (Lighthouse) | 92 🟢 | 92 🟢 |
| FCP | 6.7s 🔴 | 1.1s 🟠 |
| **LCP** | **26.5s** 🔴 | 2.1s 🟠 |
| TBT | 510ms 🟠 | 390ms 🔴 |
| CLS | 0.042 🟢 | 0.032 🟢 |
| Speed Index | 11.9s 🔴 | 1.4s 🟠 |

**Why it matters:** Most aesthetic surgery research happens on mobile. A 26s LCP means the hero (likely doctor/patient image) loads after users bounce — you’re paying for clicks that hit a blank screen.

**Top Lighthouse opportunities (mobile):**
1. **Render-blocking resources** — ~5,910 ms savings (CSS/JS in `<head>`).
2. **Cache lifetimes** — ~749 KiB (browser caching headers for static assets).
3. **Legacy JavaScript** — ~58 KiB.
4. **Font display** — ~150 ms (use `font-display: swap`).
5. **Image delivery** — ~60 KiB (WebP/AVIF, responsive sizes, preload LCP image).

**No CrUX field data** — site may lack enough Chrome real-user traffic; lab scores are all we have until Search Console CWV report is reviewed.

---

### Structured data & rich results

Source: [Rich Results Test](https://search.google.com/test/rich-results/result?id=aRjljgA4NG9sKrCEr6pYEw)

| Detected | Rich result eligible? |
|----------|----------------------|
| Breadcrumbs | ✅ 1 valid item |
| LocalBusiness / Physician / MedicalBusiness | ❌ Not detected |
| FAQ / Review snippets | ❌ Not detected |

**Issues in current schema (AIOSEO):**
- `Organization` / `WebSite` **name** is `artformplasticsurgery.com` instead of **Art Form Plastic Surgery**.
- No `Physician` entity for Dr. Kieliszak (credentials, `medicalSpecialty`, `sameAs`).
- No `MedicalClinic` with `address`, `geo`, `openingHours`, `telephone`, `hasMap`.
- No `aggregateRating` tied to GBP (must follow Google guidelines — only if reviews are on-page).
- Homepage `WebPage` description is a **dump of body copy** — not a clean meta description.

Exported snapshot: `schema-current.json`

---

### JavaScript errors & plugin bloat

Live crawl (Rich Results “Tested page”) shows:

```
Uncaught TypeError: Class extends value undefined is not a constructor or null
  → elementor-pro/assets/js/preloaded-elements-handlers.min.js (v3.15.0)
```

**Detected plugins (homepage):**
`all-in-one-seo-pack`, `astra-sites`, `elementor`, `elementor-pro`, `feeds-for-tiktok`, `google-site-kit`, `header-footer-elementor`, `instagram-feed`, `jeg-elementor-kit`, `metform`, `omnisend`, `popup-builder`, `simple-banner`

**Third-party scripts (sample):**
- Poptin (`cdn.popt.in`)
- Popup Builder
- Google Tag Manager / Ads conversion (blocked in test by robots — normal)
- `chat.mydashmetrics.com/script.js` — **failed to load** in Google’s test

**Risk:** Elementor + Elementor Pro version mismatch, overlapping popups (Poptin + Popup Builder), and 134 page resources — classic WordPress performance debt.

**Stack inference:** WordPress on **Hostinger** (LiteSpeed, PHP 8.2.30), likely built by an agency or freelancer using **Elementor Pro + Astra/Jeg kit** — not a lightweight custom theme.

---

### SEO & on-page

| Issue | Detail |
|-------|--------|
| Weak title tag | `Home - artformplasticsurgery.com` — wastes SERP space; should be keyword + brand |
| Meta conflation | Meta description appears concatenated with hero/button text in schema |
| E-E-A-T | Board certification stated — ensure dedicated **About / credentials** page is linked and schema’d |
| “0+ Happy Patients” / “0+ Years” | Counters may be JS-dependent — bad for trust if visible before animation runs |
| Typo in content | “hyperhydrosis” → hyperhidrosis (testimonial — minor) |
| Blog | Exists in nav — audit posting frequency & internal links to money pages |

---

### Google Ads vs organic branding

From SERP observation (Jun 3, 2026):

| | Organic | Paid ad |
|--|---------|---------|
| URL shown | `artformplasticsurgery.com` | `artformplasticsurgery.com` (display) |
| Ad deep link | — | `www.artformplasticsurgery.com/dr-kieliszak/consultation` |
| Favicon | ✅ Custom | ❌ Generic globe |
| Extensions | Sitelinks | About Dr. K, Gallery, Services, Payment Plans |

**Favicon on ads:** Google often pulls ad favicons from the **domain root** over time. The globe icon usually means: new/uncrawled asset, **www vs non-www** inconsistency, or missing **square favicon** in Search Console / site settings. Organic proves the asset exists (`150x150` PNG in `/wp-content/uploads/`).

**Action:** Verify Search Console property for both host variants; ensure `link rel="icon"` on all landing templates; align ad final URLs to canonical `https://artformplasticsurgery.com/...` paths.

**Note:** `/dr-kieliszak/consultation` returned **404** on non-www during scan; `/book-consultation/` returns **200** with favicon. Confirm which URL ads actually land on — possible broken or redirected path on `www` only.

---

### Google Business Profile — social gaps

GBP lists only **Instagram** and **TikTok**. Missing if they exist:
- Facebook (often expected for 35+ demographic)
- YouTube (procedure explainers, BAA video)
- LinkedIn (professional referrals)

Adding verified social profiles can improve trust and cross-signals.

---

### Social media — TikTok

- Handle: [@faceplasticsurgeon](https://www.tiktok.com/@faceplasticsurgeon)
- **~486 followers** despite heavy posting; top video **~1,872 views**
- **Insight:** Volume ≠ reach. Likely needs hook testing, SEO captions, trending audio strategy, or repurposing top performers to Reels/Shorts with paid boost.

Instagram is the stronger channel for this demographic; TikTok may still be worth it for top-of-funnel if production cost is low.

---

### Security & privacy (medical practice)

| Item | Status |
|------|--------|
| SSL | ✅ Valid until Jul 2026 |
| CSP | `upgrade-insecure-requests` only — basic |
| `X-Powered-By: PHP/8.2.30` | Exposed — minor info leak |
| HIPAA | **Not assessed** — need to know: patient portal, EMR, form data storage, BAAs with Hostinger/Omnisend/Metform |
| wp-json REST API | Public (standard WP) — ensure user enumeration not exposed |

---

### Accessibility (PSI)

Score **78** (mobile) — common Elementor issues: contrast, heading order, alt text on decorative vs content images, focus states on mobile menu. Worth manual keyboard + screen reader pass on **Book Consultation** form (Metform).

---

## Technical scan summary (automated, Jun 3 2026)

```
Host:           artformplasticsurgery.com (canonical)
Server:         LiteSpeed / Hostinger
PHP:            8.2.30
Cache:          LiteSpeed Cache (HIT)
Homepage size:  ~264 KB HTML
JSON-LD:        Yes (AIOSEO)
Page builder:   Elementor + Elementor Pro
SEO plugin:     All in One SEO Pack
Analytics:      Google Site Kit (assume GA4 + GSC)
Email:          Google Workspace + Mailgun (SPF)
SSL expiry:     2026-07-18
www redirect:   → non-www ✅
robots.txt:     ✅ Sitemap declared
```

---

## Screaming Frog crawl (Jun 3, 2026)

**282 URLs** crawled in ~17s (CLI headless, free licence). Exports: `crawl-screaming-frog/`.

| Finding | Detail |
|---------|--------|
| Internal HTML URLs | 267 |
| 4xx errors (internal pages) | **0** |
| 200 / 301 | 265 / 2 |
| Title pattern | Almost all: `{Page} - artformplasticsurgery.com` |
| Duplicate titles | `/non-surgical-procedures/` + `/non-surgical-procedures-2/` |
| Missing H1 | book-consultation, contact, about, services, blog, payment-plans, many others |
| Largest payloads | Hero JPGs + Elementor screenshot thumbnails |

**Ahrefs:** Free Site Explorer requires **domain verification** — cannot audit until client adds you in GSC or DNS. Use GSC + Screaming Frog + manual checks instead.

See `crawl-screaming-frog/CRAWL-SUMMARY.md` for re-run command.

---

## Trust-damaging content (verified)

High-ticket medical practices cannot afford visible template errors.

| Issue | Example URL |
|-------|-------------|
| **0+ counters** | Homepage, `/non-surgical-procedures-2/` | <--- this may start at 0, but it is a counter - I assume you have a strategy for this?>
| **Placeholder text** | `/functional/` — “This is the text for ‘Split ear lobe repair’…” |
| **“Plastic Suegery”** | `/services/`, `/testimonials/` |
| **“Get a Free Estimate”** | `/services/`, `/testimonials/` (use **Consultation**) |
| **“Dr. Keliszak”** typo | `/meet-dr-kieliszak/`, `/testimonials/` |
| **Wrong phone** | `/meet-dr-kieliszak/` lists **813-434-3238** (canonical: **563-3735**) |

### NAP / phone inconsistency

| Number | Source |
|--------|--------|
| **(813) 563-3735** | GBP, homepage, contact — **use everywhere** |
| 813-434-3238 | Meet Dr page |
| 813-565-3735, 813-588-5150 | Third-party directories (per citation research) |
| Stale **Vivify Plastic Surgery** | WebMD/Vitals — prior brand cleanup needed |

---

## Schema — full target list (underbuilt today)

Rich Results: **Breadcrumbs only.** Should implement:

`Physician` · `MedicalBusiness` / `LocalBusiness` · `Organization` · `Service` · `FAQPage` · `BreadcrumbList` · `VideoObject` · `ImageObject` · `PostalAddress` · `OpeningHoursSpecification` · `sameAs` (social + GBP)

Fix AIOSEO organization name from `artformplasticsurgery.com` → **Art Form Plastic Surgery**.

---

## Ads & compliance (health-sensitive category)

Audit **before** changing ads, remarketing, or form automations:

- Google Ads conversion tracking · call tracking · enhanced conversions  
- Remarketing audiences (cosmetic surgery = restricted)  
- GA4 event data · chat/form PHI · SMS consent · cookie consent  
- HIPAA vendor BAAs · before/after photo consent · testimonial consent  

Terms page includes SMS STOP/HELP language — good baseline.

---

## 5-phase improvement plan

| Phase | Focus |
|-------|--------|
| **1 — Immediate** | Phones, typos, counters, placeholder, “Free Estimate” → Consultation, favicon/ads URLs, UTMs |
| **2 — Speed** | Plugin cleanup, Elementor update, hero preload, defer JS, delay popups/chat, retest mobile PSI |
| **3 — Schema/SEO** | Physician/clinic schema, FAQs, service page depth, local city pages, internal linking |
| **4 — Citations** | Directory audit, Vivify cleanup, NAP, GBP services/Q&A/posts, local links |
| **5 — Automation** | Missed-call SMS, form auto-response, nurture, reviews, financing reminders, monthly dashboard |

**Phase 2 audits (after tomorrow):** NAP/citations · SSL Labs · securityheaders.com · `site:` index review · DMARC · manual a11y · form test · HIPAA form review.

---

## Recommended additional audits (fuller picture)

Use this as a checklist for tomorrow and follow-up weeks.

### Requires client access (high value)
| Audit | Tool / method | Why |
|-------|---------------|-----|
| Google Search Console | GSC | Queries, indexing, CWV, manual actions |
| GA4 + Ads | GA4, Google Ads | Conversion paths, CPA, landing page bounce |
| Google Ads account | Ads UI | Quality Score, search terms, wasted spend, conversion tracking |
| GBP Insights | Business Profile | Calls, direction requests, photo views |
| Email (Omnisend) | Omnisend | List health, automations, HIPAA alignment |
| EMR / practice software | On-site | What can sync: appointments, reminders, reviews |
| Cherry / financing | Portal | Lead handoff from Payment Plans page |
| Call tracking | CallRail / etc. | Attribute calls to ads vs organic |

### Can run without login (you or us)
| Audit | Tool |
|-------|------|
| Broken links | ✅ Screaming Frog (Jun 3) — 0 internal 4xx |
| Full sitemap URL inventory | SF crawl or sitemap parse |
| Competitor SERP | Local pack for “rhinoplasty Tampa”, “facelift Safety Harbor” |
| NAP citations | BrightLocal / manual Yelp/Healthgrades/Zocdoc |
| Backlink profile | Ahrefs / Semrush |
| SSL deep scan | [SSL Labs](https://www.ssllabs.com/ssltest/) |
| Security headers | [securityheaders.com](https://securityheaders.com) |
| Mobile-friendly | Google Mobile-Friendly Test |
| HIPAA marketing checklist | Internal checklist for forms & email |
| Content gap | Compare service pages vs top 3 competitors |
| Review sentiment | Export GBP reviews — themes for ads & landing pages |
| Image weight audit | Per-template hero sizes on mobile |
| Form UX test | Submit test lead on Book Consultation |
| Email auth | MXToolbox SPF/DKIM/DMARC |
| Page indexation | `site:artformplasticsurgery.com` operator review |
| Screaming Frog crawl | ✅ 282 URLs — see `crawl-screaming-frog/` |

### API / automated (completed or queued)
| Check | Status |
|-------|--------|
| HTTP headers & SSL | ✅ Done |
| DNS MX/SPF/verification | ✅ Done |
| Homepage plugin fingerprint | ✅ Done |
| JSON-LD extraction | ✅ Done |
| robots.txt | ✅ Done |
| PageSpeed (user-provided) | ✅ Documented |
| Rich Results (user-provided) | ✅ Documented |
| www / consultation URL probe | ✅ Done (404/redirect issues noted) |
| Screaming Frog CLI crawl | ✅ Done — 282 URLs, exports in `crawl-screaming-frog/` |
| Trust content scan | ✅ Placeholder, typos, wrong phone, Free Estimate |

---

**On-site checklist:** `MEETING-PREP.md` (bring tomorrow).

---

## Automation opportunities (for office visit)

**Goal:** Map what they do manually today → what software they already pay for → quick wins.

### Likely quick wins
1. **Review request automation** — post-consult / post-op SMS/email → Google review (they already have stellar ratings; systematize growth).
2. **Lead routing** — Metform / consultation form → CRM + instant SMS to coordinator + calendar link.
3. **Omnisend sequences** — welcome, consultation reminder, procedure prep, follow-up (confirm HIPAA).
4. **Social repurposing** — TikTok → IG Reels → YouTube Shorts (batch monthly).
5. **Popup consolidation** — Poptin + Popup Builder → one tool; exit-intent for consultation only.
6. **Reporting dashboard** — Site Kit + Ads + GBP calls in one weekly email.
7. **Performance package** — image CDN, critical CSS, defer non-critical JS, fix Elementor Pro error.

### Questions to ask tomorrow
- What happens when someone submits **Book Consultation**? (email only vs CRM)
- Who manages **Google Ads**? In-house or agency? Monthly spend?
- **EMR / patient management** name? (ModMed, PatientNow, etc.)
- How are **before/after gallery** photos approved and published?
- Is **Omnisend** actively used or installed-only?
- What is **mydashmetrics.com** chat supposed to do? Is anyone monitoring it?
- **Cherry** — embedded application or link-out?
- Staff roles: who answers phone, DMs, reviews?
- Any **HIPAA** concerns with current forms/popups?

---

## Priority recommendations (ranked)

### P0 — Do first (revenue & trust)
1. Fix **mobile LCP** — preload hero, WebP, reduce render-blocking CSS, audit Elementor asset loading.
2. Fix **Elementor Pro JS error** — update Elementor + Pro to matched versions.
3. Resolve **ad landing URL** + favicon consistency; confirm consultation path works.
4. Rewrite **homepage title/meta** for “Facial plastic surgeon Safety Harbor / Tampa” + brand.

### P1 — SEO & local (30 days)
5. Add **Physician + MedicalClinic** JSON-LD (both locations, phone, hours, sameAs social).
6. Fix AIOSEO **organization name** to Art Form Plastic Surgery.
7. Expand GBP social links; post weekly GBP updates tied to blog/TikTok.
8. Citation audit — ensure NAP identical on Healthgrades, RealSelf, Yelp, etc.

### P2 — Growth & automation (60–90 days)
9. Consolidate popups/chat; implement call + form automation.
10. TikTok strategy: quality over quantity OR paid spark ads on top 3 videos.
11. Content plan: procedure pages (rhinoplasty, facelift) with FAQs + schema.
12. Accessibility pass on booking funnel.

---

## Links & evidence

- **GitHub (audit + rebuild source):** https://github.com/Knight-Logics/High-Prospective-Clients/tree/master/Art-Form-Plastic-Surgery
- Website (live): https://artformplasticsurgery.com/
- PageSpeed: https://pagespeed.web.dev/analysis/https-artformplasticsurgery-com/3c8pk00hbx?form_factor=desktop
- Rich Results: https://search.google.com/test/rich-results/result?id=aRjljgA4NG9sKrCEr6pYEw
- Instagram: https://www.instagram.com/faceplasticsurgeon/
- TikTok: https://www.tiktok.com/@faceplasticsurgeon

---

*Next file: `MEETING-PREP.md` — printable checklist for office visit.*
