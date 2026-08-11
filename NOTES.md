# Gabs Lobo Website — Project Notes

## Live Site
- **URL:** https://gabslobo.com
- **Hosting:** GitHub Pages (free)
- **Repo:** https://github.com/BrandenBedoya/gabslobo-website
- **Domain Registrar:** Squarespace (DNS pointing to GitHub)
- **Branch:** `main` → deploys automatically on every push

## Tech Stack
- Pure HTML/CSS/JS — single file (`index.html`)
- Fonts: Playfair Display (serif) + Outfit (sans) via Google Fonts
- Icons: Font Awesome 6.5.1 (CDN) — Instagram, TikTok, YouTube, Amazon in footer
- No frameworks, no build step — edit `index.html` and push to deploy

## File Structure
```
index.html          ← main website (all HTML, CSS, JS in one file)
CNAME               ← tells GitHub Pages to use gabslobo.com
Assets/
  LOreal-logo.png
  garnier-logo.svg
  la-roche-posay-logo.svg
  active-logo.png
  bobbi-brown-logo.jpeg
  elf-cosmetics-logo-png_seeklogo-447294.png
  elizabeth-mott-thank-me-later-logo.jpeg
  slide-jewelry-logo.webp
  final-logo-herbishh.webp
  portfolio/            ← video thumbnails, 450x800 (9:16), ~50KB each
    hair-mask.jpg
    product-unboxing.jpg
    skin-prep.jpg
    night-routine.jpg
    first-impression.jpg
    before-after.jpg
    dog-supplements.jpg
    pet-accessories.jpg
```

### How the video thumbnails were made
Amazon creator videos (`a.co/d/...`) redirect to `amazon.com/live/video/<id>`. That page
embeds a `<script type="application/ld+json">` VideoObject with a `thumbnailUrl` — a
vertical still of the video. Steps to add a new one:
1. `curl -sLo /dev/null -w '%{url_effective}'` the short link to get the canonical URL
2. Fetch that page (it's gzipped) and pull `thumbnailUrl` out of the JSON-LD block
3. Some thumbs are 1206x2622 PNGs with black letterbox bars baked in — crop the bars off,
   then resize to 450x800 and save as JPEG q82 (keeps each file ~50KB)

## Sections (in order)
1. **Navbar** — fixed, scrolls to sections, mobile hamburger menu
2. **Hero** — Gabi's photo, headline, CTA buttons
3. **About** — bio + 3 stat cards (60+ Reels, 125k+ Views, 8+ Partnerships)
4. **Portfolio** — tabbed iPhone phone-frame video grid (2 tabs below)
5. **Services** — 5 service cards (Video UGC, Photo UGC, Unboxing, Tutorial, Stories)
6. **Brands** — auto-scrolling logo carousel (pauses on hover)
7. **Contact** — dark section with Email Me button + email address
8. **Footer** — Instagram, TikTok, YouTube, Amazon icons + copyright

### Footer social links
| Platform | URL |
|---|---|
| Instagram | https://www.instagram.com/gabslobo__ |
| TikTok | https://www.tiktok.com/@gabslobo_ |
| YouTube | https://www.youtube.com/@Gabsloboo |
| Amazon Storefront | https://a.co/d/02YYw133 |

The `.instagram` / `.tiktok` / `.youtube` / `.amazon` classes are semantic hooks only —
all styling comes from `.footer-social-link`, so a new platform just needs the matching
`fab fa-*` Font Awesome icon.

## Portfolio Tabs
**Skincare & Routine** (6 videos)

| Label | Amazon link |
|---|---|
| Hair Mask | https://a.co/d/04gtpj1q |
| Product Unboxing | https://a.co/d/0hyEyb5j |
| Skin Prep | https://a.co/d/08PNvfQt |
| Night Routine | https://a.co/d/0dOOqTBK |
| First Impression | https://a.co/d/07OIKvcn |
| Before & After | https://a.co/d/03LWbvOA |

**Pet Care** (2 videos — more to come as Gabi records them)

| Label | Amazon link |
|---|---|
| Dog Supplements | https://a.co/d/0eTAU760 |
| Pet Accessories | https://a.co/d/0aSCWzEa |

Each card uses an iPhone phone-frame CSS mockup (Dynamic Island, side buttons, rounded screen).
The whole card is an `<a>` (class `phone-wrap`) opening the Amazon video in a new tab.

### Adding a video / category
- Card markup: `<a class="phone-wrap" href="AMAZON_URL" target="_blank" rel="noopener noreferrer">`
  wrapping `.phone-frame` → `.phone-island` + `.phone-screen` (thumbnail as inline
  `background-image`) → `.portfolio-card-play`, then the `.portfolio-card-label` span.
- A new tab needs a `<button class="tab-btn" data-tab="NAME">` plus a panel with
  `id="tab-NAME"` — the JS wires them by that name, nothing else to change.
- **Panels with fewer than 3 cards** should use `class="portfolio-grid grid-center"` so the
  cards center instead of sitting left-aligned in a 3-column grid.
- Don't add per-card `background` shorthand rules — the shorthand resets `background-size`
  and breaks the `cover` crop that `.phone-screen` sets.

## Brand Carousel
Auto-scrolls (CSS animation, 35s loop, pauses on hover). 9 brands, duplicated into two
identical sets for the seamless `translateX(-50%)` loop — **add every new logo to BOTH sets**:
- L'Oréal, Garnier, La Roche-Posay, e.l.f. Cosmetics, Bobbi Brown, ACTIVE, Slide,
  Thank Me Later, Herbishh

Logos render grayscale at 55% opacity, full color on hover. `.brand-logo img` is capped at
`max-width: 175px` so wide wordmarks (Garnier) don't stretch their tile wider than the rest.
Garnier + La Roche-Posay logos are public-domain SVGs from Wikimedia Commons.

## DNS Records (Squarespace → GitHub Pages)
| Type  | Name | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| CNAME | www  | brandenbedoya.github.io |

## To-Do / Future Updates
- [x] Add real Amazon video links to all portfolio cards — done, all 8 cards link out
- [x] Add Herbishh logo — `Assets/final-logo-herbishh.webp`
- [x] Swap placeholder card backgrounds for real video thumbnails — done, `Assets/portfolio/`
- [ ] Add more Pet Care videos as Gabi records them (2 so far)
- [ ] Possibly bring back GRWM / Product Reviews / Lifestyle tabs once there's real
      video for them (removed 2026-08-10 — they were all placeholder cards)
- [ ] Consider adding a Spanish-language toggle for bilingual audience

## How to Deploy Changes
```bash
cd "/Users/brandenbedoya/Workspace/GabsLobo Website"
git add -A
git commit -m "describe your change here"
git push
```
GitHub Pages rebuilds automatically — live within ~60 seconds.

## Color Palette
```
--cream:      #FEFAF5   (page background)
--mauve:      #C4908B   (primary accent)
--mauve-dark: #B07F7A   (hover state)
--gold:       #D4B896   (secondary accent, eyebrows)
--dark:       #2A2A2A   (headings, dark text)
--mid:        #6B5B52   (body text)
--light:      #EDD9C8   (soft accent)
```
