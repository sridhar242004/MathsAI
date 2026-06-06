<div align="center">

<!-- HERO BANNER -->
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=220&section=header&text=Neural%20Conjecture%20Proposer&fontSize=42&fontColor=e8c040&animation=fadeIn&fontAlignY=38&desc=AI-Powered%20Mathematical%20Conjecture%20Generation%20Engine&descAlignY=58&descSize=16&descColor=a8a8c4"/>
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=7,11,20&height=220&section=header&text=Neural%20Conjecture%20Proposer&fontSize=42&fontColor=e8c040&animation=fadeIn&fontAlignY=38&desc=AI-Powered%20Mathematical%20Conjecture%20Generation%20Engine&descAlignY=58&descSize=16&descColor=a8a8c4" alt="Neural Conjecture Proposer"/>
</picture>

<!-- BADGES — ROW 1: Status -->
<p>
  <img src="https://img.shields.io/badge/status-production-34d399?style=for-the-badge&logo=statuspage&logoColor=white" alt="Status"/>
  <img src="https://img.shields.io/badge/version-2.0.0-c9a227?style=for-the-badge&logo=semver&logoColor=white" alt="Version"/>
  <img src="https://img.shields.io/badge/license-MIT-7c3aed?style=for-the-badge&logo=opensourceinitiative&logoColor=white" alt="License"/>
  <img src="https://img.shields.io/badge/PRs-welcome-00d4f5?style=for-the-badge&logo=github&logoColor=white" alt="PRs Welcome"/>
</p>

<!-- BADGES — ROW 2: Stack -->
<p>
  <img src="https://img.shields.io/badge/Groq-LPU%20Inference-F55036?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyeiIvPjwvc3ZnPg==&logoColor=white" alt="Groq"/>
  <img src="https://img.shields.io/badge/LLaMA_3.3-70B%20Versatile-4f9cf9?style=flat-square&logo=meta&logoColor=white" alt="LLaMA 3.3"/>
  <img src="https://img.shields.io/badge/MathJax-3.x-0a7b3c?style=flat-square&logo=latex&logoColor=white" alt="MathJax"/>
  <img src="https://img.shields.io/badge/Chart.js-4.4-ff6384?style=flat-square&logo=chartdotjs&logoColor=white" alt="Chart.js"/>
  <img src="https://img.shields.io/badge/Bootstrap-5.3-7952b3?style=flat-square&logo=bootstrap&logoColor=white" alt="Bootstrap"/>
  <img src="https://img.shields.io/badge/Vanilla_JS-ES2022-f7df1e?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript"/>
</p>

<!-- QUICK NAV -->
<p>
  <a href="#-demo"><strong>Demo</strong></a> ·
  <a href="#-overview"><strong>Overview</strong></a> ·
  <a href="#-architecture"><strong>Architecture</strong></a> ·
  <a href="#-features"><strong>Features</strong></a> ·
  <a href="#-quick-start"><strong>Quick Start</strong></a> ·
  <a href="#-configuration"><strong>Config</strong></a> ·
  <a href="#-api-reference"><strong>API</strong></a> ·
  <a href="#-contributing"><strong>Contribute</strong></a>
</p>

</div>

---

## 🎥 Demo

> **Add your demo video here** — replace the placeholder below with your actual video URL or GIF.

<!-- Option A: Embed a GitHub-hosted video -->
https://user-images.githubusercontent.com/YOUR_USER_ID/YOUR_VIDEO_ID.mp4

<!-- Option B: YouTube embed (uncomment and fill in your video ID) -->
<!--
<div align="center">
  <a href="https://youtu.be/YOUR_VIDEO_ID">
    <img src="https://img.youtube.com/vi/YOUR_VIDEO_ID/maxresdefault.jpg" width="720" alt="Demo Video"/>
  </a>
  <br/>
  <em>Click to watch the full walkthrough</em>
</div>
-->

---

## 🔭 Overview

**Neural Conjecture Proposer** is a zero-backend, single-file web application that harnesses Groq's LPU inference engine and large language models to generate novel, mathematically rigorous conjectures across all core domains of mathematics — in real time, from your browser.

It is designed for researchers, educators, and mathematically curious minds who want to explore the frontier of AI-assisted mathematical discovery.

```
Input:  Domain + Type + Complexity + Optional Context
           │
           ▼
    Groq LPU Inference  ─────────────────► LLaMA 3.3-70B (default)
           │
           ▼
    Structured Parser  (regex + section extraction)
           │
           ├── Title + Statement (LaTeX)
           ├── Motivation
           ├── Related Results
           ├── Proof Approaches
           ├── Difficulty Classification
           └── Keywords
                  │
                  ▼
        MathJax Renderer  ──►  Typeset HTML output
                  │
                  ▼
      localStorage Persistence  ──►  Analytics + History
```

> **No server. No database. No build step.** Drop the HTML file anywhere — open in a browser and start generating.

---

## 🏗 Architecture

### System Design

```
┌─────────────────────────────────────────────────────────────┐
│                     Browser (Client Only)                    │
│                                                             │
│  ┌──────────────┐   ┌──────────────┐   ┌────────────────┐  │
│  │   UI Layer   │   │ State Engine │   │  Persistence   │  │
│  │              │   │              │   │                │  │
│  │  Navbar      │   │  S = { }     │   │ localStorage   │  │
│  │  Hero        │◄──│  apiKey      │──►│  ncp_h (hist)  │  │
│  │  6 Tab Pages │   │  model       │   │  ncp_s (cfg)   │  │
│  │  Toast/Modal │   │  hist[]      │   │                │  │
│  └──────┬───────┘   │  charts{}    │   └────────────────┘  │
│         │           └──────┬───────┘                        │
│         │                  │                                 │
│  ┌──────▼───────────────────▼──────────────────────────┐   │
│  │              Core Logic (Vanilla JS ES2022)           │   │
│  │                                                       │   │
│  │  generateConjecture()   runBatch()   renderAnalytics() │  │
│  │  parseResp()            renderConj() renderHist()      │  │
│  │  buildSys()             buildUser()  callGroq()        │  │
│  └──────────────────────────────┬────────────────────────┘  │
│                                 │                            │
│  ┌──────────────────────────────▼────────────────────────┐  │
│  │              Third-Party Rendering Layer               │  │
│  │                                                        │  │
│  │   MathJax 3.x          Chart.js 4.4      Canvas API   │  │
│  │   (LaTeX → HTML)   (Domain/Cx/Activity)  (Particles)  │  │
│  └────────────────────────────────────────────────────────┘  │
└──────────────────────────┬──────────────────────────────────┘
                           │ HTTPS / Bearer Token
                           ▼
              ┌────────────────────────┐
              │   Groq Cloud API       │
              │                        │
              │  POST /v1/chat/        │
              │       completions      │
              │                        │
              │  ┌──────────────────┐  │
              │  │ LLaMA 3.3 70B    │  │
              │  │ LLaMA 3.1 8B     │  │
              │  │ Qwen3-32B        │  │
              │  │ Llama 4 Scout    │  │
              │  └──────────────────┘  │
              │   LPU Inference Engine │
              └────────────────────────┘
```

### File Structure

```
neural-conjecture-proposer/
│
├── index.html               # Entire application (single file)
│   │
│   ├── <head>
│   │   ├── MathJax config + CDN script
│   │   ├── Chart.js CDN
│   │   ├── Bootstrap 5.3 CSS + JS
│   │   ├── Bootstrap Icons
│   │   ├── Google Fonts (Cormorant Garamond, JetBrains Mono)
│   │   └── 1,200+ lines of custom CSS
│   │       ├── CSS Custom Properties (design tokens)
│   │       ├── Hero / Observatory section
│   │       ├── Orbital animation system
│   │       ├── Floating formula tags
│   │       ├── Perspective coordinate grid
│   │       ├── Tab pages
│   │       ├── Conjecture output cards
│   │       ├── Analytics grid + chart containers
│   │       ├── History cards
│   │       ├── Learn accordion
│   │       ├── Settings panels
│   │       └── Toast / Modal overlay
│   │
│   └── <body>
│       ├── #bgCanvas              ← WebGL-style particle field
│       ├── .nb (Navbar)           ← Fixed top, tab routing
│       ├── .hero (Observatory)    ← Full-viewport landing
│       ├── .ticker                ← Scrolling math ticker
│       ├── .app (6 Tab Pages)
│       │   ├── #tp-gen            ← Single conjecture generator
│       │   ├── #tp-batch          ← Batch (2–5 conjectures)
│       │   ├── #tp-analytics      ← Chart.js dashboard
│       │   ├── #tp-hist           ← Search/filter history
│       │   ├── #tp-learn          ← Famous conjectures + LaTeX ref
│       │   └── #tp-settings       ← API key, model, system prompt
│       ├── <footer>
│       ├── .tc (Toast container)
│       ├── .movl (Modal overlay)
│       └── <script>               ← ~700 lines core application JS
│
└── README.md
```

### Data Flow

```
User clicks "Generate Conjecture"
         │
         ▼
  1. getKey()         → reads API key from input / S.apiKey
  2. buildSys()       → interpolates system prompt template
  3. buildUser()      → composes user message from UI state
  4. callGroq()       → POST to Groq endpoint
         │
         ▼  (awaits response)
         │
  5. parseResp()      → regex-extracts 7 structured sections
  6. renderConj()     → injects sanitized HTML into #outArea
  7. MathJax.typesetPromise() → renders all $...$ and $$...$$
  8. S.hist.unshift() → prepends entry to in-memory history
  9. saveHist()       → serializes to localStorage (ncp_h)
 10. updHeroTotal()   → animates counter on hero section
```

---

## ✨ Features

### Core Generation Engine

| Feature | Detail |
|---|---|
| **Single Conjecture** | Full structured output: Title, Statement (LaTeX), Motivation, Related Results, Proof Approaches, Difficulty, Keywords |
| **Batch Generation** | 2–5 conjectures sequentially; Mixed domain mode cycles all 8 domains; Progressive rendering |
| **Streaming-Ready** | Architecture supports `stream: true` — currently set to `false` for structured parsing |
| **Temperature Control** | 0.1 → 1.5 slider; per-batch temperature drift (`0.7 + i*0.05`) ensures diversity |
| **Complexity Tiers** | Undergraduate → Graduate → Research-level → Millennium-level |
| **Custom Context** | Free-text field injected verbatim into user message |
| **System Prompt Editor** | Full override with `{domain}`, `{type}`, `{complexity}`, `{context}` placeholders |

### Supported Mathematical Domains

```
ℕ  Number Theory        ∮  Topology             ∘  Abstract Algebra
∫  Real Analysis        ₂  Combinatorics         ∇  Differential Geometry
P  Probability Theory   ∈  Set Theory
```

### Conjecture Types

`Existence` · `Inequality` · `Equivalence` · `Asymptotic` · `Classification` · `Structural` · `Open-ended`

### AI Models (Groq)

| Model | Context | Best For |
|---|---|---|
| `llama-3.3-70b-versatile` ⭐ | 128K | Best quality, default |
| `llama-3.1-8b-instant` | 128K | Speed-sensitive use |
| `meta-llama/llama-4-scout-17b-16e-instruct` | 10M | Long-context research |
| `qwen/qwen3-32b` | 32K | Precise, efficient |
| `openai/gpt-oss-120b` | — | Maximum capability |
| `openai/gpt-oss-20b` | — | Balanced |

### History & Analytics

- **Persistent history** via `localStorage` (`ncp_h` key)
- **Full-text search** across title, statement, domain, keywords
- **Domain filter** chips
- **Export/Import** as JSON — portable, framework-agnostic
- **Analytics dashboard** with Chart.js:
  - Doughnut: Domain distribution
  - Bar: Complexity breakdown
  - Line: 7-day activity
- **Favourite / Like** toggle per conjecture

### UI/UX System

- **Zero-backend**: No server, no build pipeline, no npm
- **Single HTML file**: Drop anywhere, works offline (once CDN loaded)
- **MathJax 3**: Renders `$inline$` and `$$display$$` LaTeX in all outputs
- **Keyboard shortcut**: `Ctrl+Enter` / `⌘+Enter` to generate
- **Toast notifications**: Success / error feedback with auto-dismiss
- **Responsive**: Mobile-first Bootstrap grid; navbar collapses gracefully
- **Dark theme**: Purpose-built — not a toggle. Pure `#04040a` void background

---

## 🚀 Quick Start

### Option 1 — Zero Setup (Recommended)

```bash
# 1. Clone
git clone https://github.com/YOUR_USERNAME/neural-conjecture-proposer.git
cd neural-conjecture-proposer

# 2. Open in browser — literally just this
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

### Option 2 — Local Dev Server

```bash
# Python (built-in)
python3 -m http.server 8080

# Node.js
npx serve .

# VS Code
# Install "Live Server" extension → right-click index.html → "Open with Live Server"
```

Then navigate to `http://localhost:8080`.

### Option 3 — Deploy (one command)

```bash
# Vercel
npx vercel --prod

# Netlify
npx netlify deploy --prod --dir .

# GitHub Pages — push to main, enable Pages in repo settings
# Cloudflare Pages — connect repo, build command: (none), output: /
```

### Get Your Free Groq API Key

1. Visit **[console.groq.com](https://console.groq.com)**
2. Sign up (free) → **API Keys** → **Create API Key**
3. Copy key starting with `gsk_...`
4. Paste in **Settings → API Configuration** in the app
5. Click **Test Connection** → green dot = ready ✓

> **Note:** The repository ships with a demo key for evaluation purposes. For production use and higher rate limits, always use your own key.

---

## ⚙️ Configuration

### State Object (`S`)

The entire application state lives in a single object:

```javascript
const S = {
  apiKey:    'gsk_...',                    // Groq API key
  model:     'llama-3.3-70b-versatile',   // Active model (validated against whitelist)
  endpoint:  'https://api.groq.com/...',  // API endpoint
  domain:    'Number Theory',             // Active math domain
  type:      'Existence',                 // Conjecture type
  cx:        2,                           // Complexity (1–4)
  temp:      0.7,                         // Temperature
  hist:      [],                          // Generation history
  charts:    {},                          // Chart.js instances (for destroy/rebuild)
  hFilter:   'all',                       // History domain filter
  hSearch:   '',                          // History search query
  generating: false                       // Generation lock (prevents double-click)
};
```

### localStorage Schema

```javascript
// History key: 'ncp_h'
[
  {
    id:         "1718000000000",        // Date.now().toString()
    ts:         "2024-06-10T12:00:00Z", // ISO 8601
    domain:     "Number Theory",
    type:       "Existence",
    cx:         "Graduate",
    title:      "...",
    statement:  "...",                  // May contain $LaTeX$
    motivation: "...",
    related:    "...",
    approaches: "...",
    difficulty: "Graduate",
    keywords:   ["prime numbers", "..."],
    raw:        "...",                  // Full raw API response
    liked:      false
  }
]

// Settings key: 'ncp_s'
{
  apiKey:   "gsk_...",
  model:    "llama-3.3-70b-versatile",
  endpoint: "https://api.groq.com/openai/v1/chat/completions",
  sysPmt:   "You are a world-class mathematician...",
  defDom:   "Number Theory",
  defCx:    "2"
}
```

### System Prompt Template

The default prompt enforces a strict 7-section output format. Override in **Settings → System Prompt**:

```
**CONJECTURE TITLE**: ...
**STATEMENT**: ...          ← LaTeX required here
**MOTIVATION**: ...
**RELATED RESULTS**: ...
**PROOF APPROACHES**: ...
**DIFFICULTY**: ...         ← Must be one of the 4 tiers
**KEYWORDS**: ...
```

Placeholders available: `{domain}` `{type}` `{complexity}` `{context}`

---

## 📡 API Reference

### `callGroq(systemPrompt, userMessage, options?)`

The core API call function. All generation flows through this.

```javascript
/**
 * @param {string} sys      - System prompt
 * @param {string} usr      - User message
 * @param {object} opts     - Optional overrides
 * @param {number} opts.temp    - Temperature (default: S.temp)
 * @param {number} opts.maxTok  - Max tokens (default: from UI select)
 * @returns {Promise<string>}   - Raw model response text
 * @throws {Error}              - Network errors, HTTP errors, empty responses
 */
async function callGroq(sys, usr, opts = {}) { ... }
```

**Request shape sent to Groq:**

```json
{
  "model": "llama-3.3-70b-versatile",
  "messages": [
    { "role": "system", "content": "..." },
    { "role": "user",   "content": "..." }
  ],
  "temperature": 0.7,
  "max_tokens": 1200,
  "stream": false
}
```

### `parseResp(rawText)` → `ParsedConjecture`

```javascript
/**
 * Extracts structured fields from the model's raw text output.
 * Uses regex section matching — tolerant of minor formatting variation.
 *
 * @param {string} txt
 * @returns {{
 *   title:      string,
 *   statement:  string,   // LaTeX-rich
 *   motivation: string,
 *   related:    string,
 *   approaches: string,
 *   difficulty: string,
 *   keywords:   string[],
 *   raw:        string
 * }}
 */
function parseResp(txt) { ... }
```

### `renderConj(parsed, container, domainLabel?)`

```javascript
/**
 * Injects the conjecture card HTML into a container element,
 * then triggers MathJax typesetting on that container.
 *
 * @param {ParsedConjecture} parsed
 * @param {HTMLElement}      container
 * @param {string}           [domLabel]  - Domain label override
 */
function renderConj(parsed, container, domLabel) { ... }
```

---

## 🧩 Extension Points

### Add a New Math Domain

```javascript
// 1. Add to DOMAINS array
const DOMAINS = [
  // ... existing ...
  'Graph Theory'   // ← new
];

// 2. Add a button in the HTML .dgrid section
<button class="dbtn" data-d="Graph Theory" onclick="selDomain(this)">
  <span>𝔾</span> Graph Theory
</button>
```

### Add a New Model

```javascript
// 1. Add to VALID_MODELS whitelist
const VALID_MODELS = [
  // ... existing ...
  'new-model-id-here'
];

// 2. Add a model card in the Settings HTML
<div class="mcard" data-m="new-model-id-here" onclick="selModel(this)">
  <div class="mcard-n">new-model-id-here</div>
  <div class="mcard-d">Description here</div>
</div>
```

### Enable Streaming

```javascript
// In callGroq(), change:
stream: false
// To:
stream: true
// Then consume response.body as a ReadableStream and update the DOM progressively.
// Note: parseResp() will need to be deferred until the stream closes.
```

---

## 🧪 Testing Locally

No test framework is configured (zero-dependency philosophy). Manual test checklist:

```
[ ] API key validation — Settings → Test Connection
[ ] Single generation — all 8 domains × all 7 types
[ ] LaTeX rendering — confirm $inline$ and $$block$$ both render
[ ] Batch generation — Mixed domain, count = 5
[ ] History persistence — generate → refresh page → history intact
[ ] Export/Import JSON round-trip
[ ] Analytics — Domain chart, Complexity chart, 7-day Activity
[ ] Keyboard shortcut — Ctrl+Enter triggers generation
[ ] Modal — batch card click opens full conjecture
[ ] Settings save/load — change model, save, refresh, confirm persisted
[ ] Mobile layout — navbar, hero, generator all responsive
```

---

## 🔒 Security Notes

- **API key is stored in `localStorage`** — do not deploy to shared/public machines without awareness of this.
- The key is sent only to `api.groq.com` via HTTPS. It is never logged or transmitted anywhere else.
- `san()` function strips `<script>` tags and inline event handlers from model output before injection.
- `esc()` HTML-encodes all user-controlled strings rendered into the DOM.
- No `eval()`, no `innerHTML` on raw API response without sanitization.

---

## 🤝 Contributing

Contributions are warmly welcomed. This project follows a **no-build-tool** philosophy — all PRs must keep the app self-contained in a single HTML file.

```bash
# Fork and clone
git clone https://github.com/YOUR_USERNAME/neural-conjecture-proposer.git

# Create feature branch
git checkout -b feat/your-feature-name

# Make changes in index.html
# Test manually (see checklist above)

# Commit with conventional commits
git commit -m "feat: add streaming support for real-time token output"
git commit -m "fix: handle 429 rate-limit with exponential backoff"
git commit -m "docs: add architecture diagram for batch flow"

# Push and open PR
git push origin feat/your-feature-name
```

### Commit Convention

```
feat:     new feature
fix:      bug fix
perf:     performance improvement
style:    CSS / visual change
refactor: code restructure, no behavior change
docs:     documentation only
chore:    dependency / config update
```

### Ideas for Contribution

- [ ] **Streaming output** — token-by-token render for perceived speed
- [ ] **Export to PDF** — print-ready conjecture cards
- [ ] **LaTeX copy button** — one-click copy of raw LaTeX statement
- [ ] **Conjecture rating system** — community upvotes via shared backend
- [ ] **Citation generator** — BibTeX output for referencing conjectures
- [ ] **Dark/Light theme toggle**
- [ ] **Offline mode** — cache CDN assets via Service Worker
- [ ] **Share URL** — encode conjecture params in URL hash
- [ ] **Proof attempt assistant** — follow-up prompts for proof sketching

---

## 📊 Performance

| Metric | Value |
|---|---|
| First meaningful paint | < 1.5s (CDN warm) |
| Time to interactive | < 2s |
| HTML file size | ~105 KB (unminified) |
| No. of external HTTP requests | 7 (fonts, MathJax, Chart.js, Bootstrap) |
| localStorage footprint | ~2–15 KB per 10 conjectures |
| Groq LLaMA 3.3 70B latency | ~1–3s (Groq LPU) |

---

## 📄 License

```
MIT License

Copyright (c) 2024 Neural Conjecture Proposer

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND.
```

---

## 🙏 Acknowledgements

- **[Groq](https://groq.com)** — LPU inference engine powering sub-second completions
- **[Meta AI](https://ai.meta.com/llama/)** — LLaMA 3 open model family
- **[MathJax](https://www.mathjax.org)** — Beautiful LaTeX rendering in the browser
- **[Chart.js](https://www.chartjs.org)** — Responsive analytics charts
- **[Bootstrap](https://getbootstrap.com)** — Responsive layout primitives
- **[Bootstrap Icons](https://icons.getbootstrap.com)** — Icon set
- **[Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond)** — Mathematical serif display font
- **[JetBrains Mono](https://www.jetbrains.com/lp/mono/)** — Monospace formula font

---

<div align="center">

*"Mathematics is not about numbers, equations, computations, or algorithms: it is about understanding."*
— William Paul Thurston

<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=100&section=footer" alt="footer"/>

**Neural Conjecture Proposer** · All conjectures are AI-generated and require rigorous mathematical verification.

</div>
