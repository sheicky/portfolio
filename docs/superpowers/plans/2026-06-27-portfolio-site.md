# Portfolio Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a minimal, static, single-page portfolio site for Sheick Ali Simpore inspired by karpathy.ai, deployed to GitHub Pages via GitHub Actions.

**Architecture:** Three hand-written static files (`index.html`, `style.css`, `theme.js`) served as-is with no build step. CSS custom properties drive a light/dark theme toggled by a small vanilla-JS script. A GitHub Actions workflow publishes the repo root to GitHub Pages on every push to `main`.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox), vanilla JavaScript, GitHub Pages, GitHub Actions.

## Global Constraints

- No framework, no bundler, no build step. Files served as-is.
- Single column, centered, `max-width: 720px`. Clean sans-serif system font stack.
- Semantic HTML: single `<h1>`, ordered headings, `<header>`/`<main>`/`<section>`.
- Light/dark theme via CSS custom properties on `:root` and `[data-theme="dark"]`; choice persisted in `localStorage`; first load respects `prefers-color-scheme`.
- All external links open in a new tab with `rel="noopener"`.
- Real URLs (verbatim):
  - GitHub: `https://github.com/sheicky`
  - LinkedIn: `https://www.linkedin.com/in/pensas/`
  - Substack post: `https://sheick.substack.com/p/automated-machine-learning-pipeline`
  - Email: `sheick-ali.simpore@efrei.net`
  - Zaka: `https://zaka-bf.com`
  - LLM Evaluation code: `https://github.com/sheicky/LLM_EVALUATION`
  - SaChi-ASR model: `https://huggingface.co/sheickydollar/SaChi-ASR`
  - AI Answer Engine code: `https://github.com/sheicky/ai-answer-engine`
  - Pentagram code: `https://github.com/sheicky/Pentagram`
  - Autonomous ML Agent code: `https://github.com/sheicky/Autonomous-Machine-Learning-Agent`
- Profile photo already present at `assets/profile.png`.

---

## File Structure

- `index.html` — full page markup: header, all content sections, theme-toggle button.
- `style.css` — theme variables, layout, typography, responsive rules.
- `theme.js` — read/persist theme preference, wire the toggle button.
- `.nojekyll` — disable Jekyll processing on GitHub Pages.
- `.github/workflows/deploy.yml` — CI/CD: deploy site to GitHub Pages on push to `main`.

---

## Task 1: Page markup (`index.html`)

**Files:**
- Create: `index.html`
- Create: `.nojekyll` (empty file)

**Interfaces:**
- Produces: a `<button id="theme-toggle">` element (consumed by `theme.js` in Task 3); CSS class hooks `.links`, `.entry`, `.entry-meta` (consumed by `style.css` in Task 2).

- [ ] **Step 1: Create `.nojekyll`**

```bash
touch .nojekyll
```

- [ ] **Step 2: Write `index.html`**

```html
<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sheick Ali Simpore</title>
  <meta name="description" content="Sheick Ali Simpore — founder & builder, AI engineer. Building Zaka. Personal site, projects, and writing." />
  <meta property="og:title" content="Sheick Ali Simpore" />
  <meta property="og:description" content="Founder & builder · AI engineer." />
  <meta property="og:image" content="assets/profile.png" />
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <main>
    <header class="site-header">
      <img class="avatar" src="assets/profile.png" alt="Sheick Ali Simpore" />
      <div class="intro">
        <div class="name-row">
          <h1>Sheick Ali Simpore</h1>
          <button id="theme-toggle" type="button" aria-label="Toggle dark mode">🌙</button>
        </div>
        <p class="tagline">Founder &amp; builder · AI engineer</p>
        <nav class="links" aria-label="Social links">
          <a href="https://github.com/sheicky" target="_blank" rel="noopener">GitHub</a>
          <a href="https://www.linkedin.com/in/pensas/" target="_blank" rel="noopener">LinkedIn</a>
          <a href="https://sheick.substack.com/p/automated-machine-learning-pipeline" target="_blank" rel="noopener">Substack</a>
          <a href="mailto:sheick-ali.simpore@efrei.net">Email</a>
        </nav>
      </div>
    </header>

    <section id="bio">
      <p>I'm a founder and builder working at the intersection of AI and real products. I spent three years at Caisse des Dépôts, where I migrated a 20+ tester QA stack to open source (saving €20K/year) and built an internal AI tool that flipped QA testers from writers to reviewers.</p>
      <p>I shipped 14+ AI apps during the Headstarter residency and evaluate frontier LLMs as an RLHF code expert at Outlier. I'm finishing an Engineer's degree (Master's) at Efrei Paris and am Azure certified (AZ-900, AI-900).</p>
    </section>

    <section id="now">
      <h2>Now</h2>
      <ul class="entry-list">
        <li>Building <a href="https://zaka-bf.com" target="_blank" rel="noopener">Zaka</a> — a real estate marketplace for Burkina Faso, live in 9+ cities, with every listing tied to the official land registry (SIF).</li>
        <li>On international exchange at Yuan Ze University, Taiwan — Data Science &amp; Deep Learning.</li>
      </ul>
    </section>

    <section id="experience">
      <h2>Experience</h2>
      <ul class="entry-list">
        <li class="entry"><strong>Founder &amp; CEO</strong>, <a href="https://zaka-bf.com" target="_blank" rel="noopener">Zaka</a> <span class="entry-meta">2025 — present</span><br />Real estate marketplace for Burkina Faso, wired into the official SIF land registry.</li>
        <li class="entry"><strong>QA Automation &amp; Test Engineering Apprentice</strong>, Informatique CDC <span class="entry-meta">2023 — 2026</span><br />Built an internal test automation platform; migrated the QA stack to open source and built AI tooling for BDD generation.</li>
        <li class="entry"><strong>Software Engineering Resident</strong>, Headstarter <span class="entry-meta">2024 — 2025</span><br />Shipped 14+ production AI apps: RAG pipelines, fine-tuned LLMs, autonomous agents.</li>
        <li class="entry"><strong>AI Code Expert (RLHF)</strong>, Outlier AI <span class="entry-meta">2024 — present</span><br />Run RLHF evaluations on frontier LLMs across full GitHub projects.</li>
      </ul>
    </section>

    <section id="projects">
      <h2>Projects</h2>
      <ul class="entry-list">
        <li class="entry"><strong>LLM Evaluation Platform</strong> — Streamlit + DeepEval app benchmarking Gemini Pro vs LLaMA with a RAG pipeline measuring precision, recall, and hallucination rate. <a href="https://github.com/sheicky/LLM_EVALUATION" target="_blank" rel="noopener">Code</a></li>
        <li class="entry"><strong>SaChi-ASR</strong> — OpenAI Whisper fine-tuned on Mooré, a low-resource African language, published on Hugging Face. <a href="https://huggingface.co/sheickydollar/SaChi-ASR" target="_blank" rel="noopener">Model</a></li>
        <li class="entry"><strong>AI Answer Engine</strong> — Perplexity-style answer engine on Gemini Flash 2.0 with multi-source RAG and source citations. <a href="https://github.com/sheicky/ai-answer-engine" target="_blank" rel="noopener">Code</a></li>
        <li class="entry"><strong>Pentagram</strong> — self-hosted SDXL-Turbo image generation on Modal GPUs with ~2s end-to-end latency. <a href="https://github.com/sheicky/Pentagram" target="_blank" rel="noopener">Code</a></li>
        <li class="entry"><strong>Autonomous ML Agent</strong> — LLM-driven AutoML platform with Optuna Bayesian tuning and parallel model training. <a href="https://github.com/sheicky/Autonomous-Machine-Learning-Agent" target="_blank" rel="noopener">Code</a></li>
      </ul>
    </section>

    <section id="writing">
      <h2>Writing</h2>
      <ul class="entry-list">
        <li><a href="https://sheick.substack.com/p/automated-machine-learning-pipeline" target="_blank" rel="noopener">Automated Machine Learning Pipeline</a> — a write-up on the LLM-driven AutoML agent.</li>
      </ul>
    </section>

    <footer class="site-footer">
      <p>Paris, France · <a href="mailto:sheick-ali.simpore@efrei.net">sheick-ali.simpore@efrei.net</a></p>
    </footer>
  </main>
  <script src="theme.js"></script>
</body>
</html>
```

- [ ] **Step 3: Verify it renders**

Run: `python3 -m http.server 8000` then open `http://localhost:8000`.
Expected: page shows the photo, name, tagline, links, and all sections (unstyled is fine at this point). No 404 for `assets/profile.png` in the browser console.

- [ ] **Step 4: Commit**

```bash
git add index.html .nojekyll
git commit -m "Add portfolio page markup"
```

---

## Task 2: Styling (`style.css`)

**Files:**
- Create: `style.css`

**Interfaces:**
- Consumes: markup classes from Task 1 (`.site-header`, `.avatar`, `.intro`, `.name-row`, `.tagline`, `.links`, `.entry-list`, `.entry`, `.entry-meta`, `.site-footer`, `#theme-toggle`) and the `[data-theme]` attribute on `<html>`.

- [ ] **Step 1: Write `style.css`**

```css
:root {
  --bg: #fdfdfb;
  --text: #1a1a1a;
  --muted: #6b6b6b;
  --accent: #2b6cb0;
  --border: #e6e6e3;
}

[data-theme="dark"] {
  --bg: #16181c;
  --text: #e8e8e6;
  --muted: #9a9a96;
  --accent: #7eb6ff;
  --border: #2c2f36;
}

* { box-sizing: border-box; }

html { font-size: 16px; }

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  line-height: 1.65;
  -webkit-font-smoothing: antialiased;
  transition: background 0.2s ease, color 0.2s ease;
}

main {
  max-width: 720px;
  margin: 0 auto;
  padding: 3rem 1.25rem 4rem;
}

.site-header {
  display: flex;
  gap: 1.5rem;
  align-items: center;
  margin-bottom: 2.5rem;
}

.avatar {
  width: 96px;
  height: 96px;
  border-radius: 50%;
  object-fit: cover;
  flex-shrink: 0;
}

.intro { min-width: 0; }

.name-row {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

h1 {
  font-size: 1.6rem;
  margin: 0;
  font-weight: 700;
}

.tagline {
  margin: 0.25rem 0 0.5rem;
  color: var(--muted);
}

#theme-toggle {
  background: none;
  border: 1px solid var(--border);
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  line-height: 1;
  padding: 0.3rem 0.45rem;
  color: var(--text);
}

#theme-toggle:hover { border-color: var(--accent); }

.links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.25rem 1rem;
}

a {
  color: var(--accent);
  text-decoration: none;
}

a:hover { text-decoration: underline; }

h2 {
  font-size: 1.05rem;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  color: var(--muted);
  border-bottom: 1px solid var(--border);
  padding-bottom: 0.35rem;
  margin: 2.5rem 0 1rem;
}

section p { margin: 0 0 1rem; }

.entry-list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.entry-list li { margin-bottom: 1rem; }

.entry-meta {
  color: var(--muted);
  font-size: 0.9rem;
  float: right;
}

.site-footer {
  margin-top: 3rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
  color: var(--muted);
  font-size: 0.9rem;
}

a:focus-visible,
#theme-toggle:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

@media (max-width: 520px) {
  main { padding: 2rem 1rem 3rem; }
  .site-header { flex-direction: column; text-align: center; align-items: center; }
  .name-row { justify-content: center; }
  .links { justify-content: center; }
  .entry-meta { float: none; display: block; }
}
```

- [ ] **Step 2: Verify styling**

Run: reload `http://localhost:8000`.
Expected: single centered column ≤720px, circular avatar, uppercase muted section headings with bottom borders, links in accent color, dates right-aligned on desktop. Resize below 520px → header stacks and centers, dates move below entries.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Add portfolio styling with light/dark theme variables"
```

---

## Task 3: Theme toggle (`theme.js`)

**Files:**
- Create: `theme.js`

**Interfaces:**
- Consumes: `<button id="theme-toggle">` from Task 1; `[data-theme]` on `<html>` and the dark palette from Task 2.

- [ ] **Step 1: Write `theme.js`**

```js
(function () {
  var root = document.documentElement;
  var KEY = "theme";

  function apply(theme) {
    root.setAttribute("data-theme", theme);
    var btn = document.getElementById("theme-toggle");
    if (btn) btn.textContent = theme === "dark" ? "☀️" : "🌙";
  }

  var stored = localStorage.getItem(KEY);
  var prefersDark = window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches;
  apply(stored || (prefersDark ? "dark" : "light"));

  document.addEventListener("click", function (e) {
    if (e.target && e.target.id === "theme-toggle") {
      var next = root.getAttribute("data-theme") === "dark" ? "light" : "dark";
      localStorage.setItem(KEY, next);
      apply(next);
    }
  });
})();
```

- [ ] **Step 2: Verify the toggle**

Run: reload `http://localhost:8000`.
Expected: clicking the moon/sun button flips the whole palette and swaps the icon. Reload → the chosen theme persists. With no stored value, the page follows the OS dark-mode setting.

- [ ] **Step 3: Commit**

```bash
git add theme.js
git commit -m "Add light/dark theme toggle"
```

---

## Task 4: GitHub Pages deploy workflow

**Files:**
- Create: `.github/workflows/deploy.yml`

**Interfaces:**
- Consumes: the static files at repo root (Tasks 1–3).

- [ ] **Step 1: Write `.github/workflows/deploy.yml`**

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Configure Pages
        uses: actions/configure-pages@v5
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: .
      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v4
```

- [ ] **Step 2: Verify locally (syntax)**

Run: `python3 -c "import yaml,sys; yaml.safe_load(open('.github/workflows/deploy.yml')); print('valid yaml')"`
Expected: `valid yaml`.

- [ ] **Step 3: Commit**

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Pages deploy workflow"
```

---

## Task 5: Publish and verify deployment

**Files:** none (operational task).

- [ ] **Step 1: Push to main**

```bash
git push origin main
```

- [ ] **Step 2: Enable Pages source = GitHub Actions**

In the GitHub repo: Settings → Pages → Build and deployment → Source = **GitHub Actions**. (One-time; the workflow needs this.)

- [ ] **Step 3: Verify the run**

Run: `gh run list --limit 1` (or check the Actions tab).
Expected: the "Deploy to GitHub Pages" workflow completes successfully.

- [ ] **Step 4: Verify the live site**

Open `https://sheicky.github.io/portfolio/`.
Expected: the styled portfolio loads, photo and links work, theme toggle works, no console 404s. (If asset paths 404 under the `/portfolio/` subpath, all asset/style/script references are relative — confirm they resolve; they are written relative in Task 1, so they should.)

---

## Self-Review

- **Spec coverage:** static HTML/CSS ✓ (Tasks 1–2), no build step ✓, theme toggle with persistence + `prefers-color-scheme` ✓ (Task 3), GitHub Pages + Actions CI/CD ✓ (Tasks 4–5), all content sections (Bio, Now, Experience, Projects, Writing, Links/footer) ✓ (Task 1), real URLs ✓ (Global Constraints + Task 1), profile photo ✓, accessibility (semantic HTML, single h1, alt text, focus-visible, meta description) ✓.
- **Placeholder scan:** no TBD/TODO; all file contents are complete.
- **Type consistency:** class names and the `#theme-toggle` id / `data-theme` attribute are consistent across Tasks 1–3.
