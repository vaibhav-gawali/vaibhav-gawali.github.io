# Vaibhav Gawali Blog (Jekyll + Chirpy)

This repository powers **vaibhavgawali.in** using **Jekyll** and the **Chirpy** theme.

## What this blog is about

This blog is written for software engineers who want practical, real-world guidance on building strong .NET systems. It focuses on:

1. **Engineering fundamentals** in C# and .NET.
2. **Software architecture and clean design** (SOLID, loosely coupled systems, maintainability).
3. **Performance-oriented development** (optimizations that actually matter).
4. **Testing and quality** (unit testing, effective test strategies, and reducing regressions).
5. **Day-to-day development practices** such as code reviews, event-driven patterns, and UI responsiveness.

My goal is simple: share knowledge through posts that are actionable, technically honest, and useful whether you’re building desktop apps or designing production systems.

## What’s included

1. **Post content**
   - Posts live in `_posts/`.
   - Current post count: **16**.

2. **Top-level navigation (Chirpy tabs)**
   - Navigation items are defined in `_tabs/` and rendered via Chirpy’s `site.tabs` collection.
   - Included tabs:
     - `Home` (`/`)
     - `About Me` (`/about/`)
     - `Contact` (`/contact/`)

3. **Tag and category archives**
   - Configured via `jekyll-archives` to generate:
     - `/tags/<tag>/`
     - `/categories/<category>/`

4. **Chirpy UI assets**
   - Chirpy’s compiled JS bundles are present under `assets/js/dist/`.
   - This is required for the Home page “post feed/list” to render correctly.

## Local development

### 1) Install dependencies

1. Ensure you have Ruby + Bundler installed.
2. From the repo root, run:

```bash
bundle install
```

### 2) Build the site

```bash
bundle exec jekyll build --config _config.yml
```

### 3) Preview in the browser

Jekyll outputs the site to `_site/` by default. You can preview using Python:

```bash
python3 -m http.server 4000 --directory _site
```

Then open:
- http://127.0.0.1:4000/

### Useful routes to verify
- Home (post feed): `/`
- About: `/about/`
- Contact: `/contact/`
- Tag archives example: `/tags/testing/`

## Contact configuration

1. **Sidebar social icons** are configured in `_data/contact.yml`.
2. The Contact page (tab) content is defined in `_tabs/contact.md`.

## Repo layout (quick reference)

- `_config.yml` — Jekyll + Chirpy configuration
- `_posts/` — blog posts (Markdown)
- `_tabs/` — Chirpy navigation tabs (Markdown)
- `_data/contact.yml` — social/contact options for the sidebar
- `assets/` — images, CSS, and JS assets

## License

This site uses the **Chirpy** theme (see the theme license). The blog content is licensed as configured in the site settings.
