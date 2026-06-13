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
- Icons: Font Awesome 6.5.1 (CDN) — Instagram, TikTok, Amazon in footer
- No frameworks, no build step — edit `index.html` and push to deploy

## File Structure
```
index.html          ← main website (all HTML, CSS, JS in one file)
CNAME               ← tells GitHub Pages to use gabslobo.com
Assets/
  LOreal-logo.png
  active-logo.png
  bobbi-brown-logo.jpeg
  elf-cosmetics-logo-png_seeklogo-447294.png
  elizabeth-mott-thank-me-later-logo.jpeg
  slide-jewelry-logo.webp
  final-logo-herbishh.webp
```

## Sections (in order)
1. **Navbar** — fixed, scrolls to sections, mobile hamburger menu
2. **Hero** — Gabi's photo, headline, CTA buttons
3. **About** — bio + 3 stat cards (60+ Reels, 125k+ Views, 8+ Partnerships)
4. **Portfolio** — tabbed iPhone phone-frame video grid (4 tabs below)
5. **Services** — 5 service cards (Video UGC, Photo UGC, Unboxing, Tutorial, Stories)
6. **Brands** — auto-scrolling logo carousel (pauses on hover)
7. **Contact** — dark section with Email Me button + email address
8. **Footer** — Instagram, TikTok, Amazon icons + copyright

## Portfolio Tabs
- Skincare & Routine
- GRWM (Get Ready With Me)
- Product Reviews
- Lifestyle

Each card uses an iPhone phone-frame CSS mockup (Dynamic Island, side buttons, rounded screen).

## Brand Carousel
Auto-scrolls (CSS animation, 35s loop, pauses on hover). Brands:
- L'Oréal, e.l.f. Cosmetics, Bobbi Brown, ACTIVE, Slide, Thank Me Later, Herbishh

## DNS Records (Squarespace → GitHub Pages)
| Type  | Name | Value                  |
|-------|------|------------------------|
| A     | @    | 185.199.108.153        |
| A     | @    | 185.199.109.153        |
| A     | @    | 185.199.110.153        |
| A     | @    | 185.199.111.153        |
| CNAME | www  | brandenbedoya.github.io |

## To-Do / Future Updates
- [ ] Add real Amazon video links to all portfolio cards (Gabi to provide URLs)
      → Find each `.phone-wrap` div and wrap the `.phone-frame` in an `<a href="AMAZON_URL" target="_blank">` tag
- [ ] Add Herbishh logo if/when available (currently shows as text fallback... wait, logo added: `Assets/final-logo-herbishh.webp`)
- [ ] Swap placeholder portfolio card backgrounds with real video thumbnails once provided
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
