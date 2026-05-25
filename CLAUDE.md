# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A single-page Facebook ad landing page for **TurnKey Bath Remodel** (turnkeybathremodel.com), a New Orleans bathroom remodeling company. Sister company to TurnKey Renovators (turnkeyrenovators.com) — both share the same license numbers (Residential #890459, Commercial #3667).

## Deployment

- **Repo:** `https://github.com/betchy1511-arch/turnkey-bath-landing-page`
- **Live URL:** `https://betchy1511-arch.github.io/turnkey-bath-landing-page/`
- **Deploy:** `git add . && git commit -m "..." && git push` — GitHub Pages auto-deploys from `master`, takes ~60 seconds

No build step. Pure HTML/CSS/JS — edit `index.html` and push.

## Architecture

Single file: `index.html`. All CSS is in `<style>`, all JS in a `<script>` at the bottom.

**Page sections (top to bottom):**
1. Sticky nav — logo + phone + CTA button. No nav links (keeps traffic on-page).
2. Hero — headline + bullet list + lead capture form (left/right grid)
3. Proof bar — 4 stats: 500+, 25+ years, 4.9★, 1 Day
4. Video section — 2×2 grid, autoplay muted, click to unmute + controls
5. Testimonials — 6 real customer cards (3-column grid)
6. Gallery — 10 real project photos (5×2 grid) from turnkeyrenovators.com/gallery/
7. Bottom CTA — book + call buttons
8. Footer — address, hours, phone, terms link
9. Sticky mobile bar — call + form buttons (mobile only)

**Animation system** — IntersectionObserver triggers `.visible` class on scroll. Elements use `.anim-fade`, `.anim-stagger`, `.anim-slide-right`. Proof bar numbers count up via JS (`countUp()`). Video/testimonial/gallery tiles use nth-child stagger delays in CSS.

**Video behavior** — `video` tags autoplay muted loop on load. `toggleVideo(card)` on click: first click unmutes + shows native controls, subsequent clicks toggle play/pause.

## Key Facts (do not invent — use these)

- **Phone:** (504) 513-6366
- **Address:** 3436 Magazine St Suite 414-N, New Orleans, LA 70115
- **Hours:** Mon–Sat 8am–5pm, Sun 8am–4pm
- **Google rating:** 4.9★
- **Stats:** 500+ bathrooms remodeled, 25+ years experience, most installs done in 1 day
- **Warranty:** Lifetime on acrylic products + 10-year workmanship
- **Financing:** 0% available for qualified homeowners
- **Free consultation:** $250 value

## Asset Sources

- Videos (remote): `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/` and `/2025/12/`
- Videos (local): `demo-day-cleveland.mov`, `bathroom-cleveland.mov`
- Gallery images: `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/IMG_*.jpg`
- Logo: `https://www.turnkeybathremodel.com/wp-content/uploads/2023/12/logo.png`

## Pending Integration (not yet live)

- **Form:** Replace the HTML form with GoHighLevel (LeadConnector) widget — `api.leadconnectorhq.com/widget/form/gfFoD91YKrsWMVrYtujS` is the existing embed on the main site
- **Facebook CAPI:** Pixel ID `987920936622343` already on main site — needs server-side CAPI events wired to form submissions and calls
- **Call tracking:** GHL tracking number (forward to 504-513-6366) to fire FB Lead event on call
- **GTM:** `GTM-TTL734MD` (main site) — needs to be added to landing page

## Brand Colors

```
--navy:      #021f35
--blue:      #4d98d2
--blue-dark: #3a7db8
--star:      #f5a623
--cta-red:   #e8440c  (form submit + mobile CTA)
```

## Save Deliverables To

`Downloads/01_Client-Work/TurnKey/`
