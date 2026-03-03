# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the Site

No build step exists. Open `index.html` directly in a browser, or serve locally:

```bash
python3 -m http.server 8000
```

There is no linter, formatter, or test suite.

## Architecture

Three files, no framework, no build system:

- `index.html` — all markup and content (Korean, `lang="ko"`)
- `styles.css` — all styles; no CSS variables, colors are hardcoded literals
- `script.js` — three features: smooth scroll, header scroll effect (50px threshold), and `IntersectionObserver`-based fade-in on every `<section>`

The `IntersectionObserver` in `script.js` targets all `section` elements automatically — any new `<section>` added to `index.html` gets fade-in for free.

## CSS Conventions

**Hardcoded color palette** (no CSS custom properties — keep it this way):

| Role | Value |
|------|-------|
| Primary / accent | `#2ec4b6` |
| Primary hover | `#26a69a` |
| Background (beige) | `#f5f5f0` |
| Text | `#2d2a4a` |

Sections alternate backgrounds `#ffffff` / `#f5f5f0`. Hover lifts use `transform: translateY(-10px)` on cards and `translateY(-5px)` on buttons, with `0.3s ease`. Scroll animations use `0.6s ease`.

Responsive breakpoints: `768px` (tablet) and `480px` (mobile). The nav shrinks and wraps on small screens — there is no hamburger menu.

## Adding Content

**Skill badge** — inside `.skills-list`:
```html
<div class="skill-item">
    <span class="skill-name">SKILL NAME</span>
</div>
```

**Project card** — inside `.projects-grid` (3-column grid, 4th card starts a new row):
```html
<div class="project-card">
    <h3 class="project-title">Project Title</h3>
    <p class="project-description">설명 텍스트</p>
    <div class="project-tags">
        <span class="tag">TAG</span>
    </div>
</div>
```

**New section:**
1. Add `<section id="new-id">` in `index.html`
2. Add `<li><a href="#new-id">Label</a></li>` to `.nav-menu`
3. Add CSS following the alternating background pattern

## Constraints

- Do not introduce a build system, bundler, framework, TypeScript, Sass, or preprocessors
- Do not convert hardcoded colors to CSS custom properties
- Do not add a hamburger menu
- Commit messages should be in Korean to match the existing history
