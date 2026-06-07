# Portfolio Audit — leonardosalvador.com

Analyzed from the exported static HTML source. All findings are based on the actual HTML, CSS, and JS files in the repository.

---

## 1. Current Information Architecture

The site has a flat, two-level hierarchy:

```
Work (gallery)                  ← primary entry point
├── Nubank                      ← case study
├── EBANX GO                    ← case study
├── Involves Stage | Login      ← case study
├── EBANX | Cashback            ← case study
├── L.P | Mettzer               ← case study
├── UX & UI | Elegance          ← case study
├── UX & UI | Leosoft           ← case study
├── L.P | lleos.com             ← case study
├── UX & UI | Clube da lingerie ← case study
├── PR Promotora de Crédito     ← case study
└── UX & UI | Buscacred         ← case study

About                           ← single biography page
```

There is no sub-categorization, no filtering, and no hierarchy beyond "gallery → detail." The about page and the gallery are peers at the top level.

---

## 2. Existing Pages and Navigation

### Global navigation
Two links only: **Work** and **About**, plus LinkedIn and Medium social icons.

### Pages

| File | Title in gallery | Year | Has description? |
|---|---|---|---|
| `work.html` | — | — | — |
| `about.html` | — | — | Yes (rich text) |
| `nubank-case-study.html` | Nubank | 2025 | No |
| `ebanx-go-case-study.html` | EBANX GO | 2021 | Yes |
| `involves-stage-sign-in-and-sign-up.html` | Involves Stage \| Login | 2020 | No |
| `ebanx-cashback.html` | EBANX \| Cashback → | 2020 | No |
| `mettzer.html` | L.P \| Mettzer → | 2018 | No |
| `elegance.html` | UX & UI \| Elegance → | 2016 | No |
| `leosoft.html` | UX & UI \| Leosoft → | 2015 | No |
| `lleoscom.html` | L.P \| lleos.com → | 2015 | No |
| `clube-da-lingerie.html` | UX & UI \| Clube da lingerie → | 2014 | No |
| `prpromotora-de-credito.html` | PR Promotora de Crédito → | 2014 | No |
| `buscacred.html` | UX & UI \| Buscacred → | 2012 | No |

---

## 3. Content Inventory

### Work page masthead
- Headline: *"Hey, I'm Leonardo Salvador, a Product Designer solving complex product problems"*
- Subtext: *"Experience building and scaling digital and financial products"*
- No call-to-action buttons

### About page sections (text is real content, rendered as inline-styled spans rather than semantic HTML)
- About
- What I do (bullet list: end-to-end experiences, compliance/risk/scalability, conversion, business impact)
- How I work (discovery, PM/eng/data collaboration, facilitation, alignment)
- What I care about
- Beyond work (family, Florianópolis, outdoors)
- Let's talk
- A single photo (lazy-loaded, not locally cached)

### Case study pages
- 9 of 11 have only a title (`<h1>`) and image content — no written narrative in the HTML
- EBANX GO is the only case study with a written description paragraph in the page header
- The Nubank page has a single full-width image with no text
- The EBANX GO page has a single image with a padding-bottom of 746.5% (a single very tall vertical scroll image)
- "You may also like" at the bottom of each case study shows 9–10 projects (essentially the full portfolio)

### Footer (identical across all pages)
```
Leonardo Salvador · Product Designer
leonardosalvador81@gmail.com · Linkedin
© 2026
```

---

## 4. Design Patterns Currently Used

### Platform
Adobe Portfolio "Andreas" theme — confirmed by `"theme":{"name":"andreas"}` in the `__config__` JavaScript object embedded on every page.

### CSS architecture
- Shared platform CSS: `dist/css/main.css` (minified, compiled, ~vendor-prefixed)
- Per-page theme CSS: different CDN file per page (11 distinct stylesheets in `cdn.myportfolio.com/`)
- No custom CSS authored by the site owner

### Typography
Adobe Typekit loaded via JavaScript embed (`use.typekit.net/ik/...`). Font family used: `ctwt` (a custom Typekit font).

### Layout components
- **Header**: logo image (left) → nav links (center) → social icons (right) → hamburger (far right)
- **Gallery grid**: uniform `project-cover` cards, each with a 4:3 aspect-ratio cover image, project title, and year
- **Case study layout**: full-width page header (`<h1>` + optional description) → content modules → "You may also like" grid → footer
- **About layout**: two-column tree layout (text column left, photo column right, roughly 50/50)

### JavaScript behaviors
- Lazy image loading: cover images have a 32px placeholder `src`, real image in `data-src` + `data-srcset`
- Click-to-expand lightbox for project module images
- Page transitions between pages
- Responsive hamburger navigation
- Fixed floating back-to-top button
- Safari back/forward cache workaround via `window.onpageshow` (full reload on bfcache restore)

### Tracking
Google Analytics with tracking ID `UA-174494204-1` (Universal Analytics, sunset July 2023).

---

## 5. UX Problems

### P5.1 — Case study pages lack narrative content
10 of 11 case studies have no written text explaining the problem, process, decisions, or outcomes. A recruiter landing on the Nubank page sees a title and a single image — nothing else. This is the most critical gap for a senior designer's portfolio.

### P5.2 — Inconsistent and confusing project titles
Naming follows no convention. Some titles have type prefixes ("UX & UI |", "L.P |"), some have directional arrows ("→"), some are just company names ("Nubank"). The arrow in some titles ("EBANX | Cashback →") is decorative noise in a list context where every item is already a link.

### P5.3 — 11 projects spanning 14 years dilutes the signal
Projects from 2012–2016 (Buscacred, PR Promotora, Clube da Lingerie, Leosoft, lleos.com, Elegance) coexist at the same visual weight as the 2021–2025 work. Showing 10-year-old work alongside current work suggests the portfolio hasn't been actively curated.

### P5.4 — No way to filter, sort, or categorize projects
Every project appears at equal weight in a single list. There is no differentiation between fintech case studies and personal/freelance projects, no way to surface the most relevant work for a specific type of role.

### P5.5 — No navigation within case studies
There is no back link to the gallery from within a case study (only the "Work" nav link). No previous/next project navigation. After reading a case study, the user must know to click "Work" in the header.

### P5.6 — "You may also like" is not curated
The section shows 9–10 projects, which is essentially the entire portfolio. It's algorithmically generated by Adobe Portfolio and not meaningful as a recommendation — it does not guide the visitor toward related or stronger work.

### P5.7 — Contact is buried and passive
The only contact method is an email address in the footer. The About page ends with "If you'd like to discuss product challenges... feel free to get in touch" but provides no clickable CTA. There is no contact form or prominent hire/connect button anywhere.

### P5.8 — Work page masthead is generic
The headline "Hey, I'm Leonardo Salvador, a Product Designer solving complex product problems" is friendly but the phrase "solving complex product problems" is a cliché that communicates nothing specific. No context about the type of companies, scale, or what makes this designer different from others.

### P5.9 — About page content lacks visual structure
The About page text is a single rich-text block where section titles ("About", "What I do", "How I work") are rendered using inline `font-size: 24px` spans. The content scrolls as a wall of text with no scannable visual hierarchy or spatial separation between sections.

---

## 6. Visual Design Problems

### P6.1 — Off-the-shelf theme without customization
The site uses the "Andreas" Adobe Portfolio theme with no visible customization. The portfolio container — the thing that should itself demonstrate design quality — is an unmodified template. For a Senior/Staff Product Designer positioning for complex product roles, this undermines credibility.

### P6.2 — No personal brand identity
No signature color, no distinctive typographic system, no visual language that extends across the portfolio and makes it memorable. The design could belong to any of thousands of Adobe Portfolio users.

### P6.3 — Uniform grid with no visual hierarchy
All 11 project cards are identical in size and structure. No card is visually emphasized. A visitor cannot tell from the gallery which are the featured case studies vs. older work.

### P6.4 — Inconsistent image quality and treatment
Cover images are a mix of photographs (Nubank), UI screenshots (EBANX GO), and illustrations. No consistent visual framing, background treatment, or compositional style.

### P6.5 — The EBANX GO case study renders as a 7.5× screen-height scroll
The single image in that case study has `padding-bottom: 746.5%`, meaning the page body is approximately 7–8 screens tall with only one image. This is an artifact of the image dimensions and the lack of structured layout within the case study.

### P6.6 — Legacy vendor-prefix CSS
`main.css` uses `-webkit-`, `-moz-`, `-ms-`, `-o-` prefixes throughout (e.g., for `transform`, `animation`). These are generated by Adobe Portfolio and unnecessary for any browser released after ~2015, indicating the platform CSS is dated.

---

## 7. Technical Limitations

### P7.1 — Full platform lock-in: CSS and JS cannot be modified
The site is a static export from Adobe Portfolio. The CSS (`main.css`) and JavaScript (`main.js`) are compiled, minified platform output — they are not hand-authored and cannot be meaningfully edited. Any structural change requires rebuilding outside the platform.

### P7.2 — No templating: global elements duplicated across 12 files
The header, navigation, social icons, and footer are copy-pasted identically into all 12 HTML files. Updating the nav or footer requires editing every file by hand.

### P7.3 — Google Analytics is broken (Universal Analytics sunset)
The tracking code `UA-174494204-1` is a Universal Analytics property. Google shut down UA in July 2023. Analytics have not been collecting data for at least two years.

### P7.4 — URL-encoded file names create fragile paths
Asset paths contain literal `%3F` in filenames (e.g., `dist/js/main.js%3Fcb=79b815c...`). These work because the files are actually named that way on disk, but any filesystem operation that normalizes `%3F` to `?` would break them.

### P7.5 — Sitemap referenced but does not exist
`robots.txt` declares `Sitemap: https://leonardosalvador.com/sitemap.xml` but no `sitemap.xml` exists in the repository.

### P7.6 — Per-page CSS from CDN creates hidden visual variation
Each case study loads a different CSS file from the cached `cdn.myportfolio.com/` directory. Changes to one page's visual style do not propagate to others and cannot be inspected or modified without targeting the correct per-page file.

### P7.7 — Safari bfcache workaround forces full page reloads
`window.onpageshow = function(e) { if (e.persisted) { window.location.reload(); }; }` is present on every page. This prevents the back-forward cache from working in Safari, making back-navigation slower and more expensive.

### P7.8 — External font dependency
The Typekit font is loaded from `use.typekit.net` via a JavaScript tag. If the Typekit project is deactivated or the CDN is unavailable, all text falls back to the system font. There is no local font fallback defined.

---

## 8. SEO Limitations

### P8.1 — Identical meta description across all pages
11 of 12 pages share the same `<meta name="description">`: *"Product Designer with experience building and scaling complex digital and financial products. Portfolio featuring real-world case studies across fintech and platforms."* Only EBANX GO has a page-specific description. Search engines cannot differentiate individual pages.

### P8.2 — Identical meta keywords across most pages
Most pages share the same keyword list: `Product Designer, Portfolio, UX Designer...`. Only two case studies have project-specific keywords. Keywords are a minor ranking factor today but the lack of differentiation reflects no SEO strategy.

### P8.3 — `twitter:site` credits Adobe Portfolio instead of the owner
Every page has `<meta name="twitter:site" content="@AdobePortfolio">`. Social shares of these pages credit Adobe Portfolio rather than Leonardo. This is a template remnant.

### P8.4 — Minimal indexable text content on case study pages
Most case study pages have only an `<h1>` with the project name and an image. There is no body text for search engines to index. These pages cannot rank for case-study-specific queries.

### P8.5 — Relative canonical URLs
`<link rel="canonical" href="work.html" />` uses a relative path. Canonical URLs should be absolute (`https://leonardosalvador.com/work`) to avoid ambiguity across crawl contexts.

### P8.6 — Shared og:image across multiple pages
The work gallery and most case study pages reference the same Nubank image as `og:image`. Social shares of Involves Stage, Mettzer, Elegance, etc. all show the Nubank cover photo.

### P8.7 — No structured data
No JSON-LD schema markup for `Person`, `ProfilePage`, or `CreativeWork`. Structured data would help search engines understand the content and could enable rich results.

### P8.8 — No sitemap.xml
Crawlers following the robots.txt declaration find a 404 for the sitemap.

---

## 9. Accessibility Limitations

### P9.1 — Social icon links have no accessible names
All 24 LinkedIn and Medium icon links (2 per page × 12 pages) contain only an SVG with no `aria-label`, no `<title>` inside the SVG, and no screen-reader text. Screen readers will announce them as unlabeled links.

### P9.2 — External links missing `rel="noopener noreferrer"`
All LinkedIn and Medium links open in `target="_blank"` with no `rel` attribute. Beyond a minor security risk (opener access), this also means assistive technology does not warn users a new window will open.

### P9.3 — Hamburger button is inaccessible
`<div class="hamburger-click-area js-hamburger"><div class="hamburger"><i></i><i></i><i></i></div></div>` — a `<div>` acting as a button with three empty `<i>` elements as the visual bars. No `role="button"`, no `aria-label`, no `aria-expanded`, no keyboard focus behavior guaranteed.

### P9.4 — About page sections are not semantic headings
Section labels ("About", "What I do", "How I work", "What I care about", "Beyond work", "Let's talk") are styled using inline `<span style="font-size: 24px">` inside a single rich-text blob. They are not `<h2>` or similar. Screen readers cannot navigate by heading, and the document outline is flat.

### P9.5 — Navigation is duplicated in the DOM
The navigation HTML exists twice on every page: once in `.js-responsive-nav` (off-canvas mobile) and once in `.site-header` (desktop). Screen readers encounter duplicate nav landmarks and duplicate link text without distinction.

### P9.6 — Lazy-loaded images require JavaScript to display
All project module images use a 1×1 GIF base64 placeholder as `src`, with the real URL in `data-src`. Without JavaScript, users see blank images throughout the site. No `<noscript>` fallback is present.

### P9.7 — `lang` attribute does not reflect Portuguese content
`<html lang="en-US">` is declared globally but several project titles and some content are in Portuguese (e.g., "PR Promotora de Crédito", "Clube da lingerie", "Buscacred"). No per-element `lang` override is used.

---

## 10. Recommendations for a Complete Redesign

### R01 — Replace Adobe Portfolio with a purpose-built static site

**Description**: Export all content (images, text) and rebuild the site using a modern static site tool (Astro, Next.js static export, or well-structured HTML+CSS with a build step). This removes all of the platform constraints in one decision.

| Dimension | Assessment |
|---|---|
| **Impact** | Critical — unlocks all other improvements |
| **Effort** | High |
| **Priority** | P1 |

---

### R02 — Curate the portfolio to 4–6 case studies

**Description**: Remove projects older than 8–10 years (pre-2016). Prioritize: Nubank (2025), EBANX GO (2021), Involves Stage (2020), EBANX Cashback (2020), and optionally Mettzer (2018). Retire Leosoft, lleos.com, Elegance, Clube da Lingerie, PR Promotora, and Buscacred, or archive them in a non-primary section.

| Dimension | Assessment |
|---|---|
| **Impact** | High — quality signal > quantity |
| **Effort** | Low |
| **Priority** | P1 |

---

### R03 — Write full case study narratives for selected projects

**Description**: Each case study needs structured written content: the business/user problem, the constraints, the design process, key decisions made, and measurable outcomes (metrics where available). The current image-only format conveys no process thinking.

| Dimension | Assessment |
|---|---|
| **Impact** | Critical — this is what hiring managers and recruiters evaluate |
| **Effort** | High (content work) |
| **Priority** | P1 |

---

### R04 — Migrate Analytics from Universal Analytics to GA4

**Description**: Replace `UA-174494204-1` with a GA4 Measurement ID. Analytics have been broken since July 2023.

| Dimension | Assessment |
|---|---|
| **Impact** | Medium |
| **Effort** | Very low (one-line change per page) |
| **Priority** | P1 — quick win |

---

### R05 — Fix `twitter:site` meta tag

**Description**: Change `<meta name="twitter:site" content="@AdobePortfolio">` to either `@lleos` or remove it entirely on all pages.

| Dimension | Assessment |
|---|---|
| **Impact** | Low–Medium (brand coherence on social shares) |
| **Effort** | Very low |
| **Priority** | P1 — quick win |

---

### R06 — Add unique meta descriptions per page

**Description**: Write a distinct `<meta name="description">` for each case study page that describes what the project was, the problem solved, and the designer's specific role. No two pages should share a description.

| Dimension | Assessment |
|---|---|
| **Impact** | High (SEO + social share quality) |
| **Effort** | Low |
| **Priority** | P2 |

---

### R07 — Design and implement a personal brand identity

**Description**: Define a visual system (color, typography scale, spacing, visual language for case study presentation) that reflects the designer's positioning as a Senior/Staff designer for complex product problems. The site container should itself be a demonstration of design quality.

| Dimension | Assessment |
|---|---|
| **Impact** | High (first impression, differentiation) |
| **Effort** | Medium |
| **Priority** | P2 |

---

### R08 — Add a prominent contact/hire CTA

**Description**: Add a visible contact button or section on the work page, about page, and at the end of each case study. The current approach buries email in the footer and ends the About page with passive text. A Senior designer's portfolio should have a clear conversion point.

| Dimension | Assessment |
|---|---|
| **Impact** | High (directly affects portfolio goal) |
| **Effort** | Low |
| **Priority** | P2 |

---

### R09 — Fix heading hierarchy on the About page

**Description**: Convert the inline-styled section labels ("What I do", "How I work", etc.) to proper `<h2>` elements. This fixes both accessibility (screen reader navigation) and SEO (heading structure signaling content organization).

| Dimension | Assessment |
|---|---|
| **Impact** | Medium |
| **Effort** | Low |
| **Priority** | P2 |

---

### R10 — Add accessible names to all icon links and fix the hamburger

**Description**: Add `aria-label` to all social icon `<a>` tags. Add `role="button"`, `aria-label="Open menu"`, and `aria-expanded` to the hamburger element. Add `rel="noopener noreferrer"` to all `target="_blank"` links.

| Dimension | Assessment |
|---|---|
| **Impact** | Medium (accessibility compliance) |
| **Effort** | Low |
| **Priority** | P2 |

---

### R11 — Use absolute canonical URLs

**Description**: Change all `<link rel="canonical" href="relative.html">` to absolute URLs: `<link rel="canonical" href="https://leonardosalvador.com/pagename">`.

| Dimension | Assessment |
|---|---|
| **Impact** | Low–Medium (SEO correctness) |
| **Effort** | Very low |
| **Priority** | P2 |

---

### R12 — Create sitemap.xml

**Description**: Generate and publish a `sitemap.xml` listing all indexable pages. The file is already declared in `robots.txt` but missing.

| Dimension | Assessment |
|---|---|
| **Impact** | Low–Medium (crawler discoverability) |
| **Effort** | Very low |
| **Priority** | P2 |

---

### R13 — Differentiate gallery grid with visual hierarchy

**Description**: Instead of 11 identical 4:3 cards, give the 2–3 featured case studies larger or visually distinct cards. Use size, color, or layout variation to guide the visitor's attention to the strongest work.

| Dimension | Assessment |
|---|---|
| **Impact** | Medium (first impressions, navigation) |
| **Effort** | Medium |
| **Priority** | P3 |

---

### R14 — Add prev/next navigation within case studies

**Description**: At the bottom of each case study, add navigation to the previous and next project. This keeps visitors in a reading flow rather than returning to the gallery between each case study.

| Dimension | Assessment |
|---|---|
| **Impact** | Medium (time-on-site, engagement) |
| **Effort** | Low |
| **Priority** | P3 |

---

### R15 — Add structured data markup

**Description**: Add `<script type="application/ld+json">` with `Person` schema on the About page and `CreativeWork` schema on case study pages. This enables richer search result presentation.

| Dimension | Assessment |
|---|---|
| **Impact** | Low–Medium (SEO enhancement) |
| **Effort** | Low |
| **Priority** | P3 |

---

### R16 — Eliminate duplicate DOM navigation

**Description**: The nav exists twice in the HTML on every page (off-canvas + desktop). Refactor to a single `<nav>` that adapts responsively, using `aria-hidden` or display logic rather than two separate DOM trees. This simplifies maintenance and removes duplicate landmarks.

| Dimension | Assessment |
|---|---|
| **Impact** | Medium (accessibility, maintainability) |
| **Effort** | Medium |
| **Priority** | P3 |

---

### R17 — Migrate font loading from Typekit JS embed to CSS embed

**Description**: Adobe Fonts (formerly Typekit) supports a `<link rel="stylesheet">` embed method that doesn't block rendering with a synchronous script load. This is a performance improvement and makes font loading more resilient.

| Dimension | Assessment |
|---|---|
| **Impact** | Low–Medium (performance) |
| **Effort** | Very low |
| **Priority** | P3 |

---

## Summary: Priority matrix

| ID | Recommendation | Impact | Effort | Priority |
|---|---|---|---|---|
| R01 | Rebuild as purpose-built site | Critical | High | P1 |
| R02 | Curate to 4–6 case studies | High | Low | P1 |
| R03 | Write full case study narratives | Critical | High | P1 |
| R04 | Migrate Analytics to GA4 | Medium | Very low | P1 |
| R05 | Fix `twitter:site` meta tag | Low | Very low | P1 |
| R06 | Unique meta descriptions | High | Low | P2 |
| R07 | Personal brand identity | High | Medium | P2 |
| R08 | Prominent contact/hire CTA | High | Low | P2 |
| R09 | Semantic headings on About page | Medium | Low | P2 |
| R10 | Accessible icon links + hamburger | Medium | Low | P2 |
| R11 | Absolute canonical URLs | Low | Very low | P2 |
| R12 | Create sitemap.xml | Low | Very low | P2 |
| R13 | Gallery visual hierarchy | Medium | Medium | P3 |
| R14 | Prev/next case study navigation | Medium | Low | P3 |
| R15 | Structured data (JSON-LD) | Low | Low | P3 |
| R16 | Eliminate duplicate DOM navigation | Medium | Medium | P3 |
| R17 | Migrate Typekit to CSS embed | Low | Very low | P3 |
