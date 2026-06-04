# Art Form Plastic Surgery — WAVE Accessibility Addendum

**Addendum to:** `AUDIT.md` (Jun 3–4, 2026)  
**Client:** Dr. Christopher Kieliszak — Art Form Plastic Surgery  
**URL tested:** https://artformplasticsurgery.com/ (homepage)  
**Tool:** [WAVE Web Accessibility Evaluation Tool](https://wave.webaim.org/) by WebAIM  
**Reports:**  
- https://wave.webaim.org/report#/https://artformplasticsurgery.com/  
- https://wave.webaim.org/report#/https://artformplasticsurgery.com/?gad_source=1&gad_campaignid=23879504771  
**Date:** June 4, 2026

> **Print note:** This is a **1-page addendum** — stapled behind `AUDIT.md`. No need to re-print the main audit.

---

## Executive summary

WAVE found **9 errors**, **15 contrast failures**, and **14 alerts** on the homepage (same counts with and without Google Ads `gclid` parameters). WAVE also showed a **“SCAN ERROR — synchronization issues”** banner — re-test with the [browser extension](https://wave.webaim.org/extension/) before/after fixes.

PageSpeed Insights reported **Accessibility 78** (mobile) / **74** (desktop) on the same site — that score checks a narrow automated ruleset. WAVE surfaces **contrast, missing alt text, and heading structure** that Lighthouse underweights.

For a **facial plastic surgery** practice (high-trust, older patients, consultation forms), accessibility is a **trust and conversion** issue — not only compliance (ADA Title III for public accommodations — consult counsel; this is not legal advice).

| Finding | Count | Severity |
|---------|-------|----------|
| Errors | **9** | 🔴 Fix immediately |
| Contrast errors | **15** | 🔴 Fix in rebuild |
| Alerts | **14** | 🟠 Triage by impact |
| PSI vs WAVE | **78 vs 24 hard failures** | 🟠 Below acceptable for medical YMYL |

**Rebuild opportunity:** Custom header (alt, hamburger labels), homepage hero form labels, contrast on gold CTAs — fixable in static rebuild + WordPress deploy.

---

## WAVE summary (homepage)

| Category | Count |
|----------|-------|
| **Errors** | 9 |
| **Contrast errors** | 15 |
| **Alerts** | 14 |
| Features | 13 |
| Structural elements | 50 |
| ARIA | 145 |

**Scanner note:** Online WAVE warned that **synchronization issues** may prevent accurate parsing of JS-driven pages (Elementor, popups, chat). Treat counts as **directional**; confirm with extension on `/` and `/book-consultation/`.

---

## Errors (9) — missing alternative text

**Issue:** Informative images lack `alt` text (or equivalent). Screen readers skip meaning.

**Likely on this site:**
- Hero / gallery imagery  
- Service or social embeds  
- Footer or partner logos  
- Elementor images rendered without alt  

**Impact:** WCAG failure (1.1.1 Non-text Content). Bad for gallery-heavy plastic surgery marketing.

**Fix:**
1. **Content images** — descriptive alt (procedure, context; no PHI without consent).  
2. **Decorative images** — `alt=""` (empty, not missing).  
3. **Logo** — `alt="Art Form Plastic Surgery"`.  
4. **Rebuild** — custom header logo already includes alt; audit remaining Elementor widgets.

---

## Contrast errors (15) — hero, nav & CTAs

**Issue:** Text/background combinations fail WCAG contrast minimums (4.5:1 normal text, 3:1 large text).

**Likely on Art Form (gold-on-black brand):**
- Gold nav links (`#b89856`) on black header  
- White/gold headline text over hero photography (no solid scrim)  
- **Book Consultation** / **Call** buttons  
- Gold **Request Consultation** on consult form column  
- Announcement bar, footer links, form placeholders  

**Impact:** Low-vision and mobile users in bright light cannot read CTAs — lost consultations.

**Fix in rebuild:**
- Darken gold for small text OR use solid button fills  
- Add scrim behind hero copy  
- Re-test with WAVE **Contrast** tab or [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)  
- Target **WCAG AA** on all buttons, phone links, and form labels  

---

## Alerts (14) — top priorities

| Alert | Count | What it means | Priority |
|-------|-------|---------------|----------|
| **Skipped heading level** | 3 | Heading order jumps (e.g. h2 → h4) | P1 — ties to missing H1 in `AUDIT.md` |
| **Redundant link** | 4 | Adjacent links to same URL | P1 |
| **Redundant title text** | 4 | `title` duplicates visible text | P2 |
| **Noscript** | 3 | Fallback may be incomplete | P2 |

### Heading structure (connects to main audit)

WAVE + Screaming Frog align — **weak hierarchy sitewide:**

- Homepage may have styled headings that are **not** a true `<h1>`  
- **Missing H1** on `/book-consultation/`, `/services/`, `/about-us/`, and others (see `AUDIT.md` crawl table)  
- **Skipped levels** confuse screen readers and dilute SEO  

**SEO + accessibility:** One clear `<h1>` per page; logical `h2` → `h3` order. Rebuild should enforce on homepage; fix Elementor templates on money pages.

### ARIA: 145 attributes

High ARIA count is typical for **Elementor + mega menus + popups** — compensating for non-semantic HTML. Not automatically wrong, but **145 on one homepage** signals complexity. Simpler markup in rebuild reduces reliance on ARIA.

---

## PSI vs WAVE — why scores disagree

| Tool | Accessibility score | What it measures |
|------|---------------------|------------------|
| **PageSpeed Insights** | **78** mobile / **74** desktop | Lighthouse subset (~40 automated checks) |
| **WAVE** | **9 errors + 15 contrast + 14 alerts** | Errors, contrast, alerts with visual overlay |

Lighthouse can pass while **contrast, alt text, and headings** still fail WAVE. Use **both**: PSI for CWV/performance (`AUDIT.md`), WAVE for accessibility depth.

---

## Related finding in `AUDIT.md` (not WAVE, but same meeting)

**Google Ads favicon (globe vs logo):** Paid ad uses `/dr-kieliszak/consultation` → **HTTP 404**. Organic uses homepage → favicon works. Fix ad final URL to `/book-consultation/` + 301 redirect. See `AUDIT.md` § Google Ads vs organic branding.

---

## Recommended fixes (ranked)

### P0 — Rebuild / immediate
1. Fix **9 missing alt** images on homepage template  
2. Fix **contrast** on Book, Call, nav, and form submit (top 5–8 flags first)  
3. One `<h1>` per page; fix skipped heading levels on homepage  

### P1 — Forms & navigation
4. Label all hero + Metform consultation fields; keyboard-test mobile menu  
5. Remove redundant adjacent links in header/footer  
6. Run WAVE extension on `/book-consultation/` (not scanned in this pass)  

### P2 — Ongoing
7. Re-test after Elementor Pro update (JS error in `AUDIT.md`)  
8. Manual screen-reader pass (NVDA/VoiceOver) on booking flow  
9. Optional: formal WCAG 2.2 AA audit if legal/compliance requested  

---

## What to say in the meeting (30 seconds)

> “PageSpeed gave you a 78 on accessibility, but WAVE found 9 missing image descriptions, 15 contrast problems on your gold buttons and hero text, and broken heading structure. For patients researching surgery on their phones — often 45 and up — that’s worth fixing. I brought a one-page addendum stapled behind the main audit; we don’t need to re-print everything.”

---

## Evidence

| Resource | URL |
|----------|-----|
| WAVE report (homepage) | https://wave.webaim.org/report#/https://artformplasticsurgery.com/ |
| WAVE report (Ads query string) | https://wave.webaim.org/report#/https://artformplasticsurgery.com/?gad_source=1&gad_campaignid=23879504771 |
| WebAIM Contrast Checker | https://webaim.org/resources/contrastchecker/ |
| WAVE browser extension | https://wave.webaim.org/extension/ |
| Main audit (companion) | `AUDIT.md` — PSI, crawl, SEO, ads favicon |
| Meeting checklist | `MEETING-PREP.md` |

**Optional print:** Screenshot of WAVE homepage overlay (Jun 4).

---

*Staple behind `AUDIT.md` · Does not replace full WCAG audit or legal ADA review.*
