# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A single-file static website for **李寓恆春的家** (Lee Home Hengchun), a vacation rental property in Hengchun, Taiwan. The entire site lives in one HTML file with all CSS and JavaScript inline.

- `李寓恆春的家_官方網站.html` — the complete website (HTML + embedded CSS + embedded JS)
- `images/` — all photos used on the site

## Development Server

```bash
python -m http.server 8080
```

Then open `http://localhost:8080/李寓恆春的家_官方網站.html`. No build step, no dependencies.

## Architecture

The single HTML file is structured in three layers:

**CSS** (inside `<style>`): All styles use CSS custom properties defined in `:root`. The design system variables are:
- Colors: `--sand`, `--earth`, `--terracotta`, `--ocean`, `--forest`, `--charcoal`, `--warm-white`, `--warm-gray`, `--cream`, `--gold`
- Typography: `--serif` (Noto Serif TC) for headings, `--sans` (Noto Sans TC) for body
- Utilities: `--shadow-sm/md/lg`, `--radius`, `--radius-sm`, `--tr` (transition)

**HTML sections** (in order): `#home` (hero) → `#advantages` → gallery strip → `#rooms` → `#explore` → `#reviews` → IG grid → `#booking` → footer → LINE FAB button

**JavaScript** (inline `<script>` at bottom):
- Navbar scroll class toggle (`nav.scrolled`)
- Mobile menu toggle (`toggleMobile()`)
- `IntersectionObserver` for `.fade-up` scroll animations
- Smooth scroll for `a[href^="#"]` links
- Room thumbnail switcher (click thumbnail → cross-fade main room image)

## Key Conventions

**Scroll animations**: Add `class="fade-up"` to any element to have it animate in on scroll. The observer watches for 8% visibility with a 30px bottom margin, staggering sibling `.fade-up` elements by 70ms each.

**Section layout pattern**: Every content section uses `.section-inner` (max-width 1200px, centered) with `.section-label` (small uppercase), `.section-title` (serif heading), and `.section-desc` (body description).

**Image paths**: All images reference `images/<filename>`. Some images still use Chinese filenames (e.g., `images/5廚房.jpg`), while newer ones use English (e.g., `images/kitchen-stove.jpg`). Both conventions are in use.

**Contact details in the page**:
- LINE: `@leehome2021` / `@leehouse`
- Phone: `0910-524177`
- Email: `leehome2021@gmail.com`
- Address: 恆南路2巷86弄71號，恆春鎮，屏東縣
- Legal registration: 屏東縣政府合法民宿編號 1124
- Instagram/Facebook: `leehome2021`

**Pricing placeholder**: The price shown as `NT$ X,XXX` is intentionally left as a placeholder — update with real pricing before publishing.
