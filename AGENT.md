# AGENT.md

Guidance for AI agents (and humans) working in this repository.

## What this is

Personal website for Taylor Chien, served via **GitHub Pages** at the custom
domain **`www.taypc6.com`**. It is a static site with **no build step**.

## Layout

- `docs/` — the published site. GitHub Pages is configured to serve from this
  folder on the `main` branch.
  - `docs/index.html` — the home page. Deliberately kept clean: name +
    tagline, a menu linking to the sub-pages, and contact links. Nothing else
    lives here.
  - `docs/site.css` — the **single site-wide theme**, shared by every page
    including the blog. Same-origin local file (no CDN), so the site still
    works offline. It defines the base look (`.site-header`, `.container`,
    `.entry-title`, `.prose`, `.site-footer`, the blog post list) plus a few
    main-page-only components (`.pagelist`, `.contact-list`, `.cv-entry`,
    `.skill-grid`, `.proj-list`). Change the theme here.
  - `docs/fonts/` — the shared self-hosted fonts (Jost, Source Serif 4),
    referenced by `site.css`. Used across the whole site.
  - `docs/about/`, `docs/resume/`, `docs/projects/` — the content sub-pages,
    each an `index.html` for a clean URL (`/about/`, `/resume/`, `/projects/`).
    They share `site.css` and repeat the same header/footer. `resume/` holds
    experience + education + skills; `projects/` holds projects + research;
    `about/` holds the bio. Links between the main pages are **root-relative**
    (`/resume/` etc.) so the header/footer markup is identical on every page;
    the current page is marked `aria-current="page"`.
  - `docs/blog/` — the "Technical Ramblings" blog: `index.html` (post listing),
    one static `<slug>.html` per post, `style.css`, and `images/` (post
    images). These posts were recovered from the Internet Archive's capture of
    the old Squarespace site at `tchien.com` (the Squarespace/WordPress XML
    export and the browser page-saves both came back as empty JS shells).
    Source of truth for the recovery was the archived RSS feed. Posts are plain
    static HTML now — edit them directly. The blog's `style.css` is just
    `@import url("../site.css");` — the blog HTML keeps linking `./style.css`,
    but the actual styles live in the shared `site.css`.
  - `docs/CNAME` — custom-domain config for Pages (`www.taypc6.com`). Must live
    alongside the published content, i.e. inside `docs/`.
- `README.md`, `AGENT.md` — repo docs. **Not** part of the published site; keep
  them at the repo root, out of `docs/`.

## Conventions

- **Theme:** the whole site shares one look — a reproduction of the old
  Squarespace (Brine/Clarkson) site: black background, white serif body
  (Source Serif 4 → Minion Pro → Georgia stack), green Futura-style headings
  (Jost), site title "Computer Systems Enthusiast". Colors/metrics came from
  the archived compiled site CSS. Keep new content in that idiom and reuse the
  existing classes in `site.css` (`.entry-title`, `.prose`, `.cv-entry`, …).
- **Self-contained:** no CDNs or external fonts/JS frameworks. Everything is a
  local, same-origin asset (`site.css`, `docs/fonts/`) so the site works
  offline. Inline the small bits of per-page JS.
- **Accessibility:** respect `prefers-reduced-motion` (disable smooth scroll
  under it — handled in `site.css`).
- **Content status:** most copy is light placeholder mapped to résumé sections.
  Real content can be brought in from the LaTeX résumé project at
  `~/git/resume` (`RESUME.md` is the content baseline). Canonical email is
  `taylor@taypc6.com`.

## Deploying

Commit to `main` and push. The `.github/workflows/deploy.yml` GitHub Actions
workflow publishes the `docs/` folder to GitHub Pages on every push to `main`
(and can be run manually from the Actions tab). There is nothing to build.

This requires the repo's Pages source to be set to **GitHub Actions**
(Settings → Pages → Build and deployment → Source: "GitHub Actions").

To preview locally, serve the folder, e.g. `python3 -m http.server -d docs 8000`.
