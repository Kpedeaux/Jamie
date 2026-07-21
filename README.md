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
