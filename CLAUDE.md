# CLAUDE.md

This file provides guidance for AI assistants working with this repository.

## Project Overview

A personal portfolio/profile website for 박준 (Jun Park), a beginner web developer learning HTML, CSS, and JavaScript. The site is written in Korean with some English technical terms.

- **Type:** Static single-page website (no build system, no frameworks)
- **Stack:** Vanilla HTML5, CSS3, JavaScript (ES6+)
- **Language:** Korean content (`lang="ko"`)
- **Author:** jun park (brainstorm90@naver.com)

## Repository Structure

```
my-profile-site/
├── index.html      # Single-page HTML, all content and layout
├── styles.css      # All styles, ~354 lines
├── script.js       # All JavaScript behavior, ~46 lines
└── .claude/
    └── settings.local.json
```

No build step is required. The site runs by opening `index.html` directly in a browser.

## Development Workflow

### Running the site

Since there is no build system, open `index.html` in a browser directly, or serve with any static file server:

```bash
# Python
python3 -m http.server 8000

# Node (if available)
npx serve .
```

### No tooling required

- No `npm install`, no build commands, no compilation
- No linter, formatter, or test suite exists
- All changes are immediately reflected on page reload

## Code Conventions

### HTML (`index.html`)

- Semantic HTML5 structure: `<header>`, `<section>`, `<footer>`
- Sections use `id` attributes for anchor navigation: `#about`, `#skills`, `#projects`, `#contact`
- BEM-like class naming: `.nav-menu`, `.hero-content`, `.project-card`, `.project-tags`
- One `<script src="script.js">` tag at the bottom of `<body>`
- Content is in Korean; section heading labels (About, Skills, Projects, Contact) remain in English

### CSS (`styles.css`)

**Color palette (use these exact values — no CSS variables exist):**
| Role | Value |
|------|-------|
| Primary / accent | `#2ec4b6` (teal) |
| Primary hover | `#26a69a` |
| Background (beige) | `#f5f5f0` |
| Background (white) | `#ffffff` |
| Text | `#2d2a4a` (dark purple-gray) |

**Layout:**
- `.container` constrains content to `max-width: 1100px`, centered with `padding: 0 20px`
- Fixed header with `backdrop-filter: blur(10px)` and `z-index: 1000`
- Sections use `padding: 100px 0` as a standard
- Projects grid: `repeat(3, 1fr)` → collapses to `1fr` on mobile

**Responsive breakpoints:**
- `768px` — tablet adjustments (nav gaps, font sizes, single-column projects)
- `480px` — mobile (stacked nav, smaller heading sizes)

**Transition standard:** `0.3s ease` for hover effects, `0.6s ease` for scroll animations

**Hover patterns:**
- Interactive cards/buttons lift: `transform: translateY(-10px)` (cards), `translateY(-5px)` (buttons)
- Box-shadow deepens with teal tint on hover

### JavaScript (`script.js`)

- Vanilla JS only — no libraries, no modules, no `import`/`export`
- Three features, each clearly comment-headed:
  1. **Smooth scroll** — `querySelectorAll('a[href^="#"]')` with `scrollIntoView`
  2. **Header scroll effect** — changes `backgroundColor` on `window.scroll` at 50px threshold
  3. **Fade-in animations** — `IntersectionObserver` on all `section` elements
     - Initial state set via inline style: `opacity: 0`, `transform: translateY(20px)`
     - Triggered state: `opacity: 1`, `transform: translateY(0)` with `0.6s ease` transition

## Page Sections

| Section | `id` | Background | Notes |
|---------|------|------------|-------|
| Hero | *(none)* | `#ffffff` | Full-viewport, centered |
| About | `#about` | `#f5f5f0` | Text in white card |
| Skills | `#skills` | `#ffffff` | Flex row of badge cards |
| Projects | `#projects` | `#f5f5f0` | 3-column CSS Grid |
| Contact | `#contact` | `#ffffff` | Email mailto button |
| Footer | *(none)* | `#f5f5f0` | Copyright line |

## Adding Content

### Adding a skill badge

In `index.html`, inside `.skills-list`, copy the pattern:

```html
<div class="skill-item">
    <span class="skill-name">SKILL NAME</span>
</div>
```

### Adding a project card

In `index.html`, inside `.projects-grid`, copy the pattern:

```html
<div class="project-card">
    <h3 class="project-title">Project Title</h3>
    <p class="project-description">Description text here</p>
    <div class="project-tags">
        <span class="tag">TAG</span>
    </div>
</div>
```

The grid handles layout automatically; adding a 4th card will start a second row.

### Adding a new section

1. Add the `<section id="new-section">` block in `index.html`
2. Add a nav link `<li><a href="#new-section">Label</a></li>` in `.nav-menu`
3. Add CSS in `styles.css` following the alternating background pattern (`#f5f5f0` / `#ffffff`)
4. The `IntersectionObserver` in `script.js` automatically picks up all `section` elements for fade-in

## What to Avoid

- Do not introduce a build system, bundler, or framework unless explicitly requested
- Do not add `npm` / `package.json` unless the project scope changes significantly
- Do not extract the inline color values into CSS custom properties without being asked — keep the existing pattern consistent
- Do not add a mobile hamburger menu without being asked — the current nav simply wraps and shrinks on small screens
- Do not add TypeScript, Sass, or preprocessors unless asked

## Git Conventions

- Commit messages have been written in Korean (e.g., `"메인에 추가해줘"`)
- There is no enforced commit message format; match the language/tone of existing commits
- No CI/CD pipeline exists
