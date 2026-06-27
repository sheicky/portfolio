# Portfolio Site — Design

**Date:** 2026-06-27
**Owner:** Sheick Ali Simpore
**Status:** Approved (pending spec review)

## Goal

A personal portfolio website modeled on Andrej Karpathy's site (https://karpathy.ai):
deliberately minimal, single-page, fast-loading, content-first. Hosted on GitHub
Pages with a CI/CD pipeline via GitHub Actions.

## Non-Goals (YAGNI)

- No framework (React/Next/Vue), no bundler, no build step for v1.
- No CMS, no backend, no analytics, no contact form.
- No blog engine — "Writing" is a static link-list for now.

## Tech & Architecture

- **Static site:** a single `index.html` + `style.css`. One small `theme.js` for the
  light/dark toggle (vanilla JS, persists choice in `localStorage`, respects
  `prefers-color-scheme` on first load).
- **No build step.** Files are served as-is.
- **Hosting:** GitHub Pages.
- **CI/CD:** `.github/workflows/deploy.yml` — on push to `main`, upload the site as a
  Pages artifact and deploy via the official `actions/deploy-pages` flow. This gives a
  real pipeline now and leaves room to add an HTML/link-validation or minification step
  later without changing the deploy model.

### File layout

```
/
├── index.html
├── style.css
├── theme.js
├── assets/
│   └── profile.jpg        # placeholder until real photo provided
├── .github/workflows/deploy.yml
├── .nojekyll              # bypass Jekyll processing on Pages
└── README.md
```

## Design / Visual

- **Type:** clean sans-serif (system font stack — matches Karpathy's current site).
- **Layout:** single column, centered, `max-width` ~720px, generous line-height.
- **Color:** off-white background, near-black text, one accent color for links.
  Light/dark toggle inverts the palette via CSS custom properties on `:root` /
  `[data-theme="dark"]`.
- **Header:** profile photo (left or top), name as `<h1>`, one-line tagline, inline
  row of social links.
- **Sections:** each is an `<h2>` heading followed by a simple list — exactly the
  Karpathy "heading + link-list" pattern. No cards, no grids, no shadows.

## Content (sourced from resume)

1. **Header** — Name: *Sheick Ali Simpore*. Tagline: *Founder & builder · AI engineer*.
   Links: GitHub, LinkedIn, Email.
2. **Bio** — 1–2 short paragraphs condensed from the resume summary (CDC, Zaka,
   Headstarter, Outlier, Efrei; Azure certified).
3. **Now** — Building Zaka (real-estate marketplace, live in 9+ cities, tied to
   Burkina Faso's SIF land registry); international exchange at Yuan Ze University,
   Taiwan.
4. **Experience** — one line each:
   - Founder & CEO, Zaka (2025–present)
   - QA Automation & Test Engineering Apprentice, Informatique CDC (2023–2026)
   - Software Engineering Resident, Headstarter (2024–2025)
   - AI Code Expert (RLHF), Outlier AI (2024–present)
5. **Projects** — each with short blurb + Demo/Code links:
   - LLM Evaluation Platform (Streamlit + DeepEval)
   - SaChi-ASR — Whisper fine-tuned on Mooré
   - AI Answer Engine (Next.js, Gemini, RAG)
   - Pentagram — self-hosted SDXL-Turbo image generation
6. **Writing** — Substack write-up on the LLM-driven AutoML agent.
7. **Links / Contact** — LinkedIn, GitHub, email, location (Paris, France).

### Content placeholders to resolve

- Profile photo (use placeholder until provided).
- Real URLs for GitHub, LinkedIn, Substack, and per-project Demo/Code (resume lists
  them as plain text). Use `#` placeholders where unknown and flag them in the README.

## Accessibility & quality

- Semantic HTML (`<header>`, `<main>`, `<section>`, `<nav>`, headings in order).
- Sufficient color contrast in both themes; visible focus states.
- Single `<h1>`; `alt` text on the photo; `<title>` and meta description set.
- Mobile-first responsive (single column already collapses gracefully).

## Success criteria

- Loads as a static page with no console errors.
- Renders correctly on mobile and desktop.
- Light/dark toggle works and persists across reloads.
- Push to `main` triggers the Actions workflow and publishes to GitHub Pages.
