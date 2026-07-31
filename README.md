# Independence St. NOLA — static rebuild

Hand-coded static rebuild of independencestnola.com (Jamie Cicatiello, tarot / astrology / reiki, New Orleans).
Replaces a WordPress + Elementor Pro + Amelia + WooCommerce stack with six flat HTML pages.
Copy is written in Jamie's own voice, sourced from her YouTube transcripts.

## Pages

- `index.html` — home (hero, services, how a reading works, proof, Moon School, events, shop, contact)
- `readings.html` — sessions and pricing ($85 / $170 / $400 / $250), gift cards
- `events.html` — private events + business pop-ups
- `moon-school.html` — Moon School (Cosmic Softness on Skool) + Seasons in Ritual planner
- `shop.html` — ritual oils, zodiac burns, planner, gift cards
- `about.html` — Jamie's story
- `almanac/` — **The Almanac**, the site's news section (index + one page per dispatch)

## The Almanac

Dated dispatches written in Jamie's voice from her YouTube transcripts, so the site reads as the
source rather than as a repost. `almanac/index.html` is the listing; each post is a flat file at
`almanac/<slug>.html`. Every post links back to its original video.

Content is generated from `_internal/` (gitignored, so Cloudflare never serves it): `posts.py` holds
the article text as data, `build.py` emits the HTML shell, nav, footer, and BlogPosting JSON-LD,
`make_art.py` draws the hero SVGs. To add a post, add a dict to the top of `POSTS` and run
`python _internal/build.py`. Editing the generated HTML directly works too, but then the two drift.

Hero art in `img/almanac/<slug>.svg` is generated (`make_art.py`), not photographic: navy sky,
starfield, and a celestial form matched to the subject. Jamie's actual YouTube thumbnails live at
`img/almanac/<videoId>.webp` and are used only inside the "watch the original" card at the bottom
of each post and as the `og:image`, because they are loud clickbait cards and would make the section
look like a repost if used as hero images.

## Structure

- `css/style.css` — whole design system (palette from her logo: navy #104058, seafoam #8BC4C5, cream #F7F2EC, brass accent, CTA teal)
- `js/main.js` — burger menu + scroll reveal only; site works fully with JS off
- `fonts/` — self-hosted Fraunces + Inter (woff2)
- `img/` — optimized webp images actually used by the site
- `original-site-assets/` — raw harvest of every image from the old WordPress site, for reuse

## Before deploy

- `original-site-assets/` contains two watermarked Adobe Stock *preview* files (never licensed).
  Exclude the folder from the public deploy (gitignore it or move it out) so they don't ship.
- Booking buttons currently open email (Independencestnola@gmail.com) with prefilled subjects.
  If Jamie has Square Appointments, swap the mailto links for her Square booking URL.
- Planner purchase is also email-based for now; the old WooCommerce checkout is gone.
- Gift cards, Moon School, YouTube, and socials all link to her live external services.

## Local preview

`python -m http.server 8823 --directory .` (a "jamiesite" entry also exists in ~/.claude/launch.json).

## Before launch (compliance)

- Accessibility pass done 2026-07-31: skip links, focus rings, nav landmark, named/hidden card links (fix lives in `_internal/build.py`, regen after edits).
- The site collects nothing today (no forms, no analytics), so it needs no privacy policy yet. If analytics or a booking form gets added at launch, add a privacy page and footer link first (copy the pattern from crcoffeenola.com/privacy).
- A tarot shop is a public accommodation under the ADA, so keep the accessibility bar when editing: run axe on changed pages before shipping.
