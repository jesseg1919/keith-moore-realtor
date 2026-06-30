# Handoff: Keith Moore Realtor Website

A marketing site for **Keith Moore**, a residential REALTOR® with **Royal LePage NRC** serving St. Catharines and the Niagara Region. Three pages — **Home**, **About**, **Contact** — with a lead-capture contact form.

---

## What's in this bundle

```
design_handoff_keith_moore_site/
├── README.md            ← this file (self-sufficient design spec)
├── index.html           ← deployable standalone build (works as-is on Vercel/Netlify)
├── package.json         ← static-site metadata + zero-build "dev" script
├── vercel.json          ← Vercel static deploy config
├── .gitignore
└── source/              ← original design-prototype source
    ├── Keith Moore Realtor.dc.html   ← the design (single-file component)
    ├── support.js                    ← prototype runtime (renders the .dc.html)
    ├── image-slot.js                 ← drag-drop image placeholder element
    └── assets/royal-lepage-nrc-logo.jpeg
```

## About the design files

The files in `source/` are a **design reference created as an HTML prototype** — they show the intended look, copy, and behavior. They are **not** the production architecture. `Keith Moore Realtor.dc.html` is authored in a lightweight in-house component format (`<x-dc>` templates + a `Component` logic class) that is rendered at runtime by `support.js`. **Do not ship that runtime.**

`index.html` is a **fully inlined, deployable** snapshot of that prototype — drop it on any static host and it runs. Use it for an immediate deploy / preview.

**The recommended task:** recreate this design in a real codebase using its established patterns. If you're starting fresh, **Next.js (App Router) on Vercel** is the natural fit — three routes (`/`, `/about`, `/contact`), a shared header/footer layout, and a server action or form endpoint for the contact form. Match the spec below pixel-for-pixel.

## Fidelity

**High-fidelity.** Final colors, typography, spacing, copy, and interactions are all defined. Recreate the UI pixel-perfectly. Exact values are in [Design Tokens](#design-tokens) and per-component below.

---

## Design tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| Brand red | `#c8102e` | Primary CTA, accents, links, eyebrows |
| Brand red (hover) | `#a00d24` | CTA hover |
| Pink wash | `#fbeaed` | Icon tiles |
| Pink accent (on dark) | `#ff7a8c` | Eyebrow text on dark sections |
| Ink | `#161616` | Primary text, dark sections |
| Footer black | `#141414` | Footer bg |
| Body text | `#56554f` | Paragraph copy |
| Muted text | `#8a8983` / `#74736e` | Captions, legal |
| Light text (dark bg) | `#bcbbb6` / `#9b9a95` | Copy on dark |
| Off-white | `#f7f6f3` | Alternating section bg |
| Hairline | `#ebe9e5` / `#e4e2dd` / `#eee` | Borders/dividers |
| Card border | `#ebe9e5` | Cards, inputs `#d9d7d2` |
| Star gold | `#f5a623` | Review stars |
| White | `#ffffff` | Cards, base bg |

### Typography
- **Serif (display):** `Newsreader`, serif — headings, eyebrow brand name. Weights 400/500/600; italic 400 available.
- **Sans (UI/body):** `Hanken Grotesk`, sans-serif — body, nav, buttons, labels. Weights 400/500/600/700.
- Google Fonts import:
  `https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400&family=Hanken+Grotesk:wght@400;500;600;700&display=swap`
- **Headings** `Newsreader` 500, `letter-spacing:-.015em to -.02em`, `line-height:1.04–1.12`. H1 `clamp(32–62px)`, H2 `clamp(28–42px)`, H3 19px.
- **Eyebrow label:** Hanken 600, 12px, `letter-spacing:.16em`, uppercase, brand red, often preceded by a 26px×1.5px red rule.
- **Body:** Hanken 400, 15–18px, `line-height:1.6–1.7`.

### Spacing / shape
- Page max-width: **1240px** (narrower bands 760/1100px), side padding `clamp(20px,5vw,56px)`.
- Section vertical padding: `clamp(54px,7vw,108px)`.
- Radius: cards/images **14px**, large images **16px**, inputs **9px**, buttons **6–9px**, pills **30px**, icon tiles **11px**.
- Card shadow (hover): `0 24px 44px -28px rgba(0,0,0,.22)`; image shadow: `0 30px 60px -36px rgba(0,0,0,.28)`.
- Card hover lift: `translateY(-3px)`, transition `.25s`.

---

## Global layout

- **Sticky header** (`top:0; z-index:60`): translucent white `rgba(255,255,255,.88)` + `backdrop-filter:blur(12px)`, 1px bottom border `#eee`. Left: Royal LePage NRC logo (46px tall) + 1px divider + brand lockup ("Keith Moore" / "ROYAL LEPAGE NRC · REALTOR®"). Right nav: Home / About / Contact (active item has a 2px red underline) + a red **"Call Keith"** phone button.
- **Client-side page switch:** Home/About/Contact are toggled in state (`page`), not separate URLs, in the prototype. **In production, make these real routes** (`/`, `/about`, `/contact`). Nav + footer links navigate; `window.scrollTo(0,0)` on change.
- **Footer** (`#141414`): 4 columns — brand blurb + Facebook icon link, Contact (address/email/phone), Explore (nav), Service Areas — then a legal disclaimer row + copyright.

### Contact details used throughout
- Phone/text: **(905) 555-0199** → `tel:+19055550199`, `sms:+19055550199` *(placeholder — confirm real number)*
- Email: **keithmoore@royallepage.ca**
- Office: **33 Maywood Avenue, St. Catharines, ON L2R 1C5**
- Facebook: **https://www.facebook.com/keithmoore.ca**
- Service areas: St. Catharines, Fonthill, Pelham, Thorold, Welland, Niagara Region

---

## Screens

### 1. Home (`/`)
1. **Hero** — 2-col grid (`.72fr / 1.28fr`). Left: eyebrow "Residential REALTOR® · Niagara Region", H1 "Real estate guidance you can feel confident in.", intro paragraph, two CTAs ("Contact Keith" red, "Call Now" outline), and a 5-star trust row. Right: a square photo of Keith (transparent-bg cut-out), bottom-anchored, `aspect-ratio:1/1`, `max-width:620px`.
2. **Approach band** (dark `#161616`) — centered eyebrow + large serif statement.
3. **Awards & Recognition** — centered heading + a single row of four Royal LePage award logos (President's Gold 2025 & 2023, Director's Platinum 2022 & 2021). *Logos are currently hot-linked from nrcrealty.ca — see [Assets](#assets); download and self-host them.*
4. **How Keith Helps** — 4 cards (Buying, Selling, Market Value Analysis, Step-by-Step Guidance), each with a pink icon tile, serif H3, body copy. Hover lift.
5. **Why Work With Keith** (`#f7f6f3`) — image left (5:6), copy right + a 2-col checklist of 8 traits with red checkmarks.
6. **Reviews** — 3 cards, each 5 gold stars + Google "G" glyph, quote, attribution. Caption: "Placeholder reviews — to be replaced with Keith's verified Google reviews."
7. **Service Areas** (`#f7f6f3`) — copy + 6 location pills (pin icon) left, image right.
8. **Closing CTA** (dark) — heading + Contact / Call / Email buttons.

### 2. About (`/about`)
1. **Hero** — 2-col: eyebrow "About", H1 "Meet Keith Moore.", intro, "Get in Touch" + "Call Keith" CTAs; right a square professional photo (`aspect-ratio:1/1`, fade-in animation).
2. **Lifestyle row** — 3 square image placeholders, then a centered 3-paragraph bio (lead paragraph in serif).
3. **What You Can Expect** (`#f7f6f3`) — 4 value cards (Honesty, Confidentiality, Thorough Guidance, Lifetime Service).
4. **Balanced & Relatable** — copy left, a 3-image collage right (one tall 3:4 spanning two rows + two squares).
5. **Closing CTA** (dark).

### 3. Contact (`/contact`)
1. **Header band** — eyebrow "Contact", H1 "Contact Keith Moore.", intro.
2. **Contact method cards** — Call / Text / Email (tappable `tel:`/`sms:`/`mailto:`) + Office card.
3. **Form card** (white card on `#f7f6f3`). Fields: Full name*, Email*, Phone, "Do you currently own a home?" (Yes/No), **"When are you looking to move?"** (ASAP / 1–3mo / 3–6mo / 6–12mo / Just exploring), "Are you looking to…" (Buy/Sell/Both), "Preferred way to be contacted" (Phone/Text/Email), Message* (textarea). Red **Send Message** button. Note: "Submissions are sent to keithmoore@royallepage.ca".
   - On success, the card swaps to a confirmation state (check badge, "Thank you, {firstName} — your message is on its way.").
4. **Proudly Serving** band — service-area list + closing copy.

---

## Interactions & behavior

- **Nav / routing:** prototype toggles `page` state; **build as real routes.** Scroll to top on navigation.
- **Buttons/links:** all have hover states — red CTA → `#a00d24`; outline buttons invert to dark fill; cards lift `-3px` with shadow; nav text → red.
- **Contact form validation** (client-side, on submit):
  - `name` required → "Please enter your name."
  - `email` required + regex `^[^@\s]+@[^@\s]+\.[^@\s]+$` → "Please enter a valid email address."
  - `message` required → "Please add a short message."
  - Errors render in red under each field; clearing a field's value clears its error.
  - **The prototype does NOT actually send email** — it only shows the success state. **In production, wire the submit to a real handler** (e.g. a Next.js server action / API route emailing keithmoore@royallepage.ca, or a service like Resend/Formspree). The collected fields are: name, email, phone, owns, timeline, intent, contact, message.
- **Animations:** About hero image `fade-in .9s` (`@keyframes fi`). A `fu` (fade-up) keyframe is defined for optional entrance use.

## State (prototype)

`page` ('home'|'about'|'contact'), `form` (8 fields above), `errors` (per-field strings), `submitted` (bool). In production, page → router; form → form state + server submission; the rest is local UI state.

---

## Assets

- **Header logo:** `source/assets/royal-lepage-nrc-logo.jpeg` (included) — Royal LePage NRC lockup, rendered 46px tall.
- **Award logos (NOT bundled — hot-linked):** download these and self-host in `/public`, then update the `<img src>`:
  - President's Gold 2025 — `https://nrcrealty.ca/wp-content/uploads/2026/03/RLP-PresidentsGoldHz-2025-EN-RGB-300px-1.png`
  - President's Gold 2023 — `https://nrcrealty.ca/wp-content/uploads/2025/03/RLP-PresidentsGold_Hz-2023-EN-RGB-300px-1.png`
  - Director's Platinum 2022 — `https://nrcrealty.ca/wp-content/uploads/2025/03/DIRECTORS-PLATINUM-2022.png`
  - Director's Platinum 2021 — `https://nrcrealty.ca/wp-content/uploads/2025/03/DIRECTORS-PLATINUM-2021.png`
- **Keith's photos:** the prototype uses drag-drop placeholders (`<image-slot>`) — **no real photos are embedded.** Replace every image slot with Keith's real photography:
  - Home hero (square, transparent-bg cut-out preferred), Home "Why Work With Keith" (5:6), Home "Service Areas" image, About hero (square), About lifestyle ×3 (square), About collage ×3 (one 3:4 + two 1:1).
- **Icons:** all inline SVG (home, gift/handshake, bar chart, list, shield, lock, document, heart, phone, message, mail, map pin, arrow, check, star, Google "G"). Reuse or swap for the codebase's icon set (e.g. Lucide).
- **Fonts:** Google Fonts — Newsreader + Hanken Grotesk (import string above).

## Placeholders to replace before launch
- Phone **(905) 555-0199** → Keith's real number (appears in header, hero, contact cards, footer, all `tel:`/`sms:`).
- **Reviews** are placeholder copy → swap for verified Google reviews.
- **Keith's photos** → real photography (all image slots).
- **Award logos** → self-hosted copies.
- Confirm office address & email.

---

## Deploying `index.html` right now

`index.html` is self-contained and static. To preview locally: open it in a browser, or `npx serve .`. To deploy: push this folder to GitHub and import to Vercel (framework preset **Other** / static — see `vercel.json`), or `vercel deploy`. The contact form will show its success state but won't send email until wired to a backend.
