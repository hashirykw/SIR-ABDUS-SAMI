# Economics with Sir Abdul Sami — website

A front-end-only, multi-page website for **Sir Muhammad Abdul Sami** (Cambridge O Level 2281, IGCSE 0455 and AS & A Level 9708 Economics, Karachi).
No backend, no database, no API keys. Every form ends by opening **WhatsApp** with a pre-filled message. Anything the site "remembers" (theme, sound, tracker ticks, scores, flashcards, cart, timer, portal demo sign-in) lives in the visitor's own browser (`localStorage`), and the site still works if storage is blocked.

---

## Files (one flat folder — no sub-folders)

| File | What it is |
|---|---|
| `index.html` | Home: hero, method, headline → diagram story, courses, Policy Desk, diagram rail, syllabus map, timeline, study tools, places, CTA |
| `courses.html` | 2281 / 0455 / 9708 paper formats (until 2026 vs from 2027), assessment objectives, command-word flip cards, how classes run |
| `syllabus.html` | Full syllabus tracker (89 topics) with popups: key points, key terms, formulas, diagrams, common mistakes, mini-quiz |
| `diagrams.html` | Diagram Bank: 31 diagrams drawn step by step, with label checklist, what examiners want, common mistakes and practice mode |
| `past-papers.html` | Paper finder (opens PapaCambridge's public archive), score tracker with trend chart, exam timer with focus mode |
| `lab.html` | Econ Lab: 12 tools incl. S&D studio, elasticity, PPC, market structures, macro calculator, CPI basket, Lorenz/Gini, comparative advantage, exchange-rate lab, 60-question MCQ drill, 336 flashcards, essay planner |
| `notes.html` | Notes store with cart drawer and WhatsApp checkout |
| `about.html` | His story, method, philosophy, places, timeline |
| `contact.html` | Enrolment form → WhatsApp, contact cards, campus card with directions, 12-question FAQ |
| `portal.html` | **Student portal (front-end demo)** — see below |
| `404.html` | "This page has zero demand." |
| `favicon.svg` | AS monogram icon |
| `og.jpg` | Share image (1200×630) — a designed placeholder; replace it any time with your own |
| `sitemap.xml`, `robots.txt`, `vercel.json` | Hosting files (`vercel.json` turns on clean URLs) |

Every `.html` page is **self-contained**: all CSS is in its `<style>` and all JavaScript in its `<script>`. Libraries load from CDN (three.js r160 for the particle background, GSAP + ScrollTrigger, Lenis smooth scroll) and fonts from Google Fonts. If a CDN is blocked the site still works fully — just with less motion.

**Images to add later (optional):** `abdul-sami.webp` — a transparent-background portrait cutout, about 1000×1200. Until it exists, the site shows the "AS" monogram plate instead (never a broken image).

---

## Editing CONFIG

Open any page, find `const CONFIG = {` at the top of the main `<script>`. **The same CONFIG is in every page**, so when you change a value, change it in all 11 pages (use your editor's "Find in files → Replace").

| Key | What it does |
|---|---|
| `whatsapp` | Digits only, e.g. `"923001234567"`. While blank, WhatsApp buttons open WhatsApp and let the user pick the chat. |
| `phoneDisplay` | How the number is shown, e.g. `"0300 123 4567"`. The WhatsApp contact card appears once `whatsapp` is set. |
| `campusPhone`, `campusPhoneLabel` | The Professionals Core North Nazimabad enquiries number. |
| `email` | Shown on Contact when filled. |
| `social.facebook / linkedin / youtube / instagram` | Empty = icon hidden. |
| `featuredVideo` | A YouTube URL. Empty = the "Featured lecture" section stays hidden. |
| `domain` | Used for canonical links. Also find-and-replace `https://sir-abdul-sami.vercel.app` in all files when the real domain is known. |
| `places` | Cards on Home, About, Contact and the footer. Remove any place he no longer teaches at. |
| `products` | Notes store items: `title`, `level`, `pages`, `printed` price, `pdf` price (Rs.). |
| `results`, `reviews` | **Empty = sections hidden.** Add real entries only, e.g. `{ name:"", grade:"A*", level:"O Level", year:2026 }` and `{ name:"", text:"", tag:"O Level 2026" }`. |
| `portal.preview` | `true` shows "Demo" badges in the portal. |
| `portal.demoId`, `portal.demoCode` | The demo sign-in (default `AS-1001` / `econ2026`). |
| `portal.freePreviewLectures` | How many lectures visitors can watch without signing in. |

---

## The student portal (`portal.html`) — front-end demo

What it does now:
- **Sign-in screen** with Student ID + access code (demo login shown on the page), plus free preview lectures; locked lectures send visitors to WhatsApp to enrol.
- **Overview** — lectures watched, syllabus confidence (from the student's own tracker), test average, best MCQ score, continue-watching, announcements.
- **Lectures** by unit, opening in a player (YouTube unlisted link or `.mp4`; demo lectures show a placeholder), "Mark as watched".
- **Notes**, **Announcements**, **Marks** (table + trend chart), and a **Study desk** that reads the student's real tracker, past-paper scores, flashcards and MCQ best from this browser.

The lectures, notes, announcements and marks are **sample data** in the `PORTAL_DEMO` object near the top of the portal's script, and every screen carries a "Demo" badge. This is a preview to show Sir Sami; it is **not secure** — anyone can read the demo code in the page source, so don't put real student data in it.

**Going live later** needs a small backend (for example Supabase or Firebase) for real accounts, per-student marks and private files. The front-end is already laid out for it: replace `PORTAL_DEMO` and the `signIn()` check with calls to that backend. No backend code is included, by design.

---

## Deploy on Vercel (no build step)

1. Go to vercel.com → **Add New… → Project → "Deploy" by dragging this folder** (or use the Vercel CLI: `vercel` inside the folder).
2. No framework, no build command, output directory = the folder itself.
3. `vercel.json` already sets `"cleanUrls": true` so `/courses` works as well as `/courses.html`. `404.html` is used automatically for missing pages.
4. Add your domain in Vercel → Settings → Domains, then update `domain` in CONFIG and the URLs in `sitemap.xml`, `robots.txt` and each page's meta tags (find-and-replace `https://sir-abdul-sami.vercel.app`).

To preview locally just double-click `index.html` (everything except the 404 page works from your disk).

---

## Content notes

- Syllabus content and definitions are **summarised in our own words** from Cambridge International's published syllabuses (O Level 2281 and IGCSE 0455 for 2027–2029; AS & A Level 9708 for 2026–2028). All practice questions are original. Not affiliated with Cambridge. Past papers © UCLES and are linked from PapaCambridge's public archive.
- Every number on the site is either a fact from his public profiles, an official Cambridge paper format, or labelled **"practice values"** / **"Demo"**.
- **Demo prices, to be confirmed:** all notes titles and prices in `CONFIG.products` are demo values.
- Fees and class timings are never shown — every such question routes to WhatsApp.

---

## Confirm before launch

1. Name spelling: **Abdul Sami** (every public source). Confirm "Abdul" vs "Abdus".
2. His personal **WhatsApp number**: fill `CONFIG.whatsapp` and `phoneDisplay`.
3. Which institutions he **currently** teaches at. Remove any he has left from `CONFIG.places` and the timelines on Home and About.
4. Years at Highbrow College, The Ambitions, Abeel E-School and Beaconhouse, and **whether he lectured at the University of Karachi** (shown on About only, as "Former lecturer").
5. Real **results and reviews**. Those sections stay hidden until they are added.
6. Notes titles and prices (demo values).
7. YouTube, LinkedIn and Instagram links, and the featured video.
8. A higher-resolution portrait with a plain background, to make `abdul-sami.webp`, and (optionally) a custom `og.jpg`.
9. Permission before showing any institution logos. The site uses text wordmarks only.
10. The final domain. Find and replace `https://sir-abdul-sami.vercel.app`.
11. Portal: real lectures/notes/marks and secure sign-in need a backend before real students use it (see above).

---

## Tagline options

Live: **"Economics, beyond the textbook."** Also used as kickers: "Read the graph. Understand the world." · "Know it. Apply it. Argue it."

## Keyboard shortcuts

- **Ctrl + K / ⌘K or "/"** — search everything (pages, topics, diagrams, lab tools, key terms, timers; type "timer 45")
- **Esc** — close any popup; in timer focus mode, Esc asks before leaving
