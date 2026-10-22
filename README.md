# Economics with Sir Abdul Sami — website

A front-end-only website for **Sir Muhammad Abdul Sami** (Cambridge O Level 2281, IGCSE 0455 and AS & A Level 9708 Economics, Karachi).
There is no backend, no database and no API keys. Every form ends by opening **WhatsApp** with a pre-filled message. Anything the site "remembers" (theme, sound, tracker ticks, scores, flashcards, cart, timer, portal demo sign-in) is stored in the visitor's own browser (`localStorage`). The site still works if storage is blocked.

---

## Files (one flat folder, no sub-folders)

### Main pages
| File | What it is |
|---|---|
| `index.html` | Home: hero, method, headline → diagram story, courses, Policy Desk, diagram rail, syllabus map, timeline, study tools, **revision guides + key term of the day**, places, CTA |
| `courses.html` | 2281 / 0455 / 9708 paper formats (until 2026 and from 2027), assessment objectives, command-word flip cards, how classes run |
| `syllabus.html` | Syllabus tracker (89 topics) with popups: key points, key terms, formulas, diagrams, common mistakes, mini-quiz, and a link to the full guide where one exists |
| `diagrams.html` | Diagram Bank: 32 diagrams drawn step by step, grouped by level, with label checklist, what examiners want, common mistakes and a practice mode |
| `past-papers.html` | Paper finder (opens PapaCambridge's public archive), score tracker with trend chart, exam timer with focus mode |
| `lab.html` | Econ Lab: 12 tools in three groups, including the 60-question MCQ drill, 336 flashcards and the essay planner |
| `notes.html` | Notes store with cart drawer and WhatsApp checkout |
| `about.html` | His story, method, philosophy, places, timeline |
| `contact.html` | Enrolment form → WhatsApp, contact cards, campus card with directions, FAQ |
| `portal.html` | **Student portal (front-end demo).** See below. |
| `404.html` | "This page has zero demand." |

### Free study content (written to bring in search traffic)
| File | What it is |
|---|---|
| `guides.html` | Revision guide hub with search and level filter |
| `guide-*.html` (15 files) | Original revision guides. **Exam skills:** command words, evaluation, drawing diagrams, MCQ technique, 2027 changes, O Level vs IGCSE. **Micro:** PED, taxes and subsidies, market failure, market structures. **Macro:** inflation, AD/AS, fiscal/monetary/supply-side policy. **International:** exchange rates, the current account |
| `glossary.html` | Key terms A–Z: all 336 definitions as real page text, searchable, filterable by level and linked to syllabus topics |
| `formulas.html` | Formula sheet: 19 formulas, each with a worked example (practice values) and a "watch out". It can be printed. |

Each guide has live step-by-step diagrams, worked examples, exam tips, common mistakes, a three-question quick check, an FAQ, related guides and **Share on WhatsApp / Copy link** buttons. The pages carry structured data (`Article`, `BreadcrumbList`, `FAQPage`, `DefinedTermSet`), so Google can show them as rich results. All of them are listed in `sitemap.xml`.

### Other files
| File | What it is |
|---|---|
| `favicon.svg` | AS monogram icon |
| `og.jpg` | Share image (1200×630). It is a designed placeholder, so replace it with your own whenever you like. |
| `sitemap.xml`, `robots.txt`, `vercel.json` | Hosting files (`vercel.json` turns on clean URLs; `robots.txt` keeps the demo portal out of search) |

Every `.html` page is **self-contained**: all its CSS is in its `<style>` and all its JavaScript is in its `<script>`. Libraries load from CDNs (three.js r160 for the particle background, GSAP + ScrollTrigger, Lenis smooth scroll) and fonts come from Google Fonts. If a CDN is blocked, the site still works fully, just with less motion.

**Image to add later (optional):** `abdul-sami.webp`, a transparent-background portrait cutout of about 1000×1200. Until it exists, the site shows the "AS" monogram plate instead, never a broken image.

---

## Design notes

- **Liquid-glass interface.** Buttons, cards, navigation, dock, chat, popups and drawers are frosted glass over slow copper, teal and indigo glows. Light and dark themes both keep AA contrast.
- **Phones:** repeated cards (courses, method steps, tools, places, timeline, guides, diagrams, lab tools, notes, formulas, key terms, past-paper years, timer presets, table rows) become **swipe rails** with snap scrolling and page dots, so pages stay short. The syllabus tracker shows one unit at a time, with unit chips. The footer is compact. The theme, sound and search controls are also inside the menu.
- **Smoothness:** the particle field pauses while you scroll on phones and draws at 30 fps. Background glows are static on touch screens. Off-screen sections are skipped until they are near the viewport. Reduced-motion settings turn all motion off.

---

## Editing CONFIG

Open any page and find `const CONFIG = {` near the top of the main `<script>`. **Every page (29 in all) contains the same CONFIG**, so when you change a value, change it everywhere at once with your editor's "Find in files → Replace".

| Key | What it does |
|---|---|
| `whatsapp` | Digits only, e.g. `"923001234567"`. While it is blank, WhatsApp buttons open WhatsApp and let the visitor pick the chat. |
| `phoneDisplay` | How the number is shown, e.g. `"0300 123 4567"`. The WhatsApp contact card appears once `whatsapp` is set. |
| `campusPhone`, `campusPhoneLabel` | The Professionals Core North Nazimabad enquiries number. |
| `email` | Shown on Contact when filled. |
| `social.facebook / linkedin / youtube / instagram` | Empty = icon hidden. |
| `featuredVideo` | A YouTube URL. Empty = the "Featured lecture" section stays hidden. |
| `domain` | Used for canonical links and shared links. Also find-and-replace `https://sir-abdul-sami.vercel.app` in all files once the real domain is known. |
| `places` | Cards on Home, About, Contact and in the footer. Remove any place he no longer teaches at. |
| `products` | Notes store items: `title`, `level`, `pages`, `printed` price, `pdf` price (Rs.). |
| `results`, `reviews` | **Empty = sections hidden.** Add real entries only, e.g. `{ name:"", grade:"A*", level:"O Level", year:2026 }` and `{ name:"", text:"", tag:"O Level 2026" }`. |
| `portal.preview` | `true` shows "Demo" badges in the portal. |
| `portal.demoId`, `portal.demoCode` | The demo sign-in (default `AS-1001` / `econ2026`). |
| `portal.freePreviewLectures` | How many lectures visitors can watch without signing in. |

---

## The student portal (`portal.html`), a front-end demo

What it does now:
- **Sign-in screen** with Student ID and access code (the demo login is shown on the page), plus free preview lectures. Locked lectures send visitors to WhatsApp to enrol.
- **Overview:** lectures watched, syllabus confidence (from the student's own tracker), test average, best MCQ score, continue watching, announcements.
- **Lectures** by unit, opening in a player (an unlisted YouTube link or an `.mp4`; demo lectures show a placeholder), with "Mark as watched".
- **Notes**, **Announcements**, **Marks** (table and trend chart), and a **Study desk** that reads the student's real tracker, past-paper scores, flashcards and best MCQ score from this browser.

The lectures, notes, announcements and marks are **sample data** in the `PORTAL_DEMO` object near the top of the portal's script, and every screen carries a "Demo" badge. The portal is a preview to show Sir Sami. It is **not secure**: anyone can read the demo code in the page source, so don't put real student data in it.

**Going live later** needs a small backend (for example Supabase or Firebase) for real accounts, per-student marks and private files. The front end is already laid out for this: replace `PORTAL_DEMO` and the `signIn()` check with calls to that backend. By design, no backend code is included.

---

## Deploy on Vercel (no build step)

1. Go to vercel.com → **Add New… → Project**, then drag this folder in (or run `vercel` inside the folder with the Vercel CLI).
2. Choose no framework and no build command. The output directory is the folder itself.
3. `vercel.json` already sets `"cleanUrls": true`, so `/guides` works as well as `/guides.html`. Vercel uses `404.html` automatically for missing pages.
4. Add your domain in Vercel → Settings → Domains. Then update `domain` in CONFIG and replace `https://sir-abdul-sami.vercel.app` everywhere (in the pages, `sitemap.xml` and `robots.txt`).
5. **To get search traffic:** add the site to Google Search Console and submit `sitemap.xml`. Share guide links in class WhatsApp groups; each guide has a share button.

To preview locally, double-click `index.html`. Everything except the 404 page works from your disk.

---

## Content notes

- Syllabus content and definitions are **summarised in our own words** from Cambridge International's published syllabuses (O Level 2281 and IGCSE 0455 for 2027–2029; AS & A Level 9708 for 2026–2028). All practice questions, guides and worked examples are original. The site is not affiliated with Cambridge. Past papers are © UCLES and are linked from PapaCambridge's public archive.
- Every number on the site is one of these: a fact from his public profiles, an official Cambridge paper format, or a value labelled **"practice values"** / **"Demo"**. The Pakistani examples in the guides (PKR, petrol, remittances, the State Bank of Pakistan) are concept examples, not quoted statistics.
- **Demo prices, to be confirmed:** all notes titles and prices in `CONFIG.products` are demo values.
- Fees and class timings are never shown. Every such question routes to WhatsApp.

---

## Confirm before launch

1. Name spelling: **Abdul Sami** (as in every public source). Confirm "Abdul" vs "Abdus".
2. His personal **WhatsApp number**: fill in `CONFIG.whatsapp` and `phoneDisplay`.
3. Which institutions he **currently** teaches at. Remove any he has left from `CONFIG.places` and from the timelines on Home and About.
4. His years at Highbrow College, The Ambitions, Abeel E-School and Beaconhouse, and **whether he lectured at the University of Karachi** (shown on About only, as "Former lecturer").
5. Real **results and reviews**. Those sections stay hidden until entries are added.
6. Notes titles and prices (currently demo values).
7. YouTube, LinkedIn and Instagram links, and the featured video.
8. A higher-resolution portrait with a plain background, to make `abdul-sami.webp`, and (optionally) a custom `og.jpg`.
9. Permission before showing any institution logos. The site uses text wordmarks only.
10. The final domain. Find and replace `https://sir-abdul-sami.vercel.app`.
11. Portal: real lectures, notes and marks, and a secure sign-in, need a backend before real students use it (see above).
12. **Revision guides, key terms and formula sheet:** this is original study content written for the site. Ask Sir Sami to read it, and to confirm he is happy for it to appear under his name before launch.

---

## Keyboard shortcuts

- **Ctrl + K / ⌘K or "/"**: search everything (pages, guides, topics, diagrams, lab tools, key terms, timers; type "timer 45")
- **Esc**: close any popup; in timer focus mode, Esc asks before leaving
