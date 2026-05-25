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
1. Sticky nav — logo (left) + trust strip center (stars + rating) + license badges + phone + "Get a Free Consultation" button (right)
2. Hero — headline + bullet list (left) + GHL Banner Form iframe (right)
3. Proof bar — 4 stats: 500+, 25+ years, 4.9★, 1 Day
4. Video section — 2x2 grid, dark gray bg, centered heading, autoplay muted, click to unmute
5. Testimonials — 6 real customer cards (3-column grid)
6. Gallery — 10 real project photos (5x2 grid), dark navy bg, lightbox on click
7. Bottom CTA — photo background + gradient overlay, book + call buttons
8. Footer — address, hours, phone, terms link
9. Sticky mobile bar — call + form buttons (mobile only)
10. Popup modal — opens from nav "Get a Free Consultation" button, contains GHL Popup Form iframe

**Animation system** — IntersectionObserver triggers `.visible` class on scroll. Elements use `.anim-fade`, `.anim-stagger`, `.anim-slide-right`. Proof bar numbers count up via JS (`countUp()`). Video/testimonial tiles use nth-child stagger delays in CSS. Gallery tiles have NO opacity animation — always visible on load (removing it fixed a blank-space bug).

**Video behavior** — `video` tags autoplay muted loop on load. `toggleVideo(card)` on click: first click unmutes + shows native controls, subsequent clicks toggle play/pause.

**Lightbox** — clicking any gallery photo opens full-size image in dark overlay. Click outside or Escape to close.

**Modal** — nav CTA opens popup modal with GHL form. Click outside or Escape to close. Body scroll locks when open.

## GHL Forms

| Location | Form Name | Form ID |
|----------|-----------|---------|
| Hero card (right side) | Banner Form-w | `C0aHdvenmYAA0VRySz1o` |
| Nav popup modal | Popup Form-w | `wLSQ2oSWOhjgp6luyG8A` |

GHL embed script loaded once before `</body>`: `https://link.msgsndr.com/js/form_embed.js`
Iframe height set to `100%` — GHL script auto-resizes via postMessage.

## Key Facts (do not invent — use these)

- **Phone:** (504) 513-6366
- **Address:** 3436 Magazine St Suite 414-N, New Orleans, LA 70115
- **Hours:** Mon–Sat 8am–5pm, Sun 8am–4pm
- **Google rating:** 4.9★
- **Stats:** 500+ bathrooms remodeled, 25+ years experience, most installs done in 1 day
- **Warranty:** Lifetime on acrylic products + 10-year workmanship
- **Financing:** 0% available for qualified homeowners
- **Free consultation:** $250 value
- **Licenses:** Residential LA #890459, Commercial LA #3667

## Asset Sources

- Videos 1+2 (remote): `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/`
- Videos 3+4 (local MP4): `demo-day-cleveland.mp4`, `bathroom-cleveland.mp4`
- Video posters (local): `poster-demo-day.jpg`, `poster-bathroom.jpg`
- Gallery images: first 10 remote from `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/IMG_*.jpg`; 10 local jpegs committed to repo root: IMG_5425, IMG_5434, IMG_5450, IMG_5463, IMG_5464, IMG_5480, IMG_5500, IMG_5487, IMG_5498, IMG_5503
- Logo: `https://www.turnkeybathremodel.com/wp-content/uploads/2023/12/logo.png`
- Bottom CTA background image: `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/IMG_7160-scaled-1.jpg`

## Gallery

20 photos total, 4-column grid (`gallery-10` class, `repeat(4,1fr)`). Lightbox opens on click.

- Images 1-6, 9-10: remote from `https://www.turnkeyrenovators.com/wp-content/uploads/2025/03/`
- Images 7-8: local files `IMG_gallery_07.jpg` + `IMG_gallery_08.jpg` (downloaded from turnkeyrenovators.com — remote URLs broke in browser)
- Images 11-20: local jpegs (IMG_5425, IMG_5434, IMG_5450, IMG_5463, IMG_5464, IMG_5480, IMG_5500, IMG_5487, IMG_5498, IMG_5503)

**Gallery blank-space bug (FIXED 2026-05-25):** Tiles used `opacity:0` + IntersectionObserver animation. Observer only reliably triggered for the first 6 items; items 7-20 stayed invisible but still occupied grid space, creating a huge dark empty area. Fix: removed `opacity:0` entirely from `.social-video-tile` — tiles are always visible on load.

## Sticky Form (FIXED 2026-05-25)

**What was tried and failed:** JS fixed-position approach with 3s delay — unfixed too early because `leftBottomY` was the left column bottom, not the form bottom.

**What works:** CSS only.
- `.form-card` — `position: sticky; top: 90px; max-height: calc(100vh - 110px); overflow-y: auto;`
- `.hero-inner > .anim-fade` (left column) — `position: sticky; top: 90px;`
- Both columns stick together while user fills out the form. Form scrolls internally (overflow-y) so user can reach all fields.
- JS sticky block removed entirely.

## Pending / Resume Next Session

- **Local videos 3+4 not playing** — `demo-day-cleveland.mp4` and `bathroom-cleveland.mp4` may be slow from GitHub Pages. Fix: upload to `turnkeyrenovators.com/wp-content/uploads/` and update src URLs
- **Facebook CAPI:** Pixel ID `987920936622343` — needs server-side CAPI events wired to GHL form submissions and calls
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
