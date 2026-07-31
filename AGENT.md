# AGENT.md

Guidance for AI agents (and humans) working in this repository.

## What this is

Personal website for Taylor Chien, served via **GitHub Pages** at the custom
domain **`www.taypc6.com`**. It is a static site with **no build step**.

## Layout

- `docs/` — the published site. GitHub Pages is configured to serve from this
  folder on the `main` branch.
  - `docs/index.html` — the home page. Deliberately kept clean: hero (name +
    tagline), a terminal-style menu linking to the sub-pages, and contact
    links. Nothing else lives here.
  - `docs/terminal.css` — the shared terminal theme. Linked by the home page
    and every top-level sub-page. Same-origin local file (no CDN), so the site
    still works offline. The blog is the one exception — it keeps its own theme
    (`docs/blog/style.css`), see below.
  - `docs/about/`, `docs/resume/`, `docs/projects/` — the content sub-pages,
    each an `index.html` for a clean URL (`/about/`, `/resume/`, `/projects/`).
    They share `terminal.css` and repeat the same window chrome (titlebar, nav,
    footer). `resume/` holds experience + education + skills; `projects/` holds
    projects + research; `about/` holds the bio. Nav links between pages are
    relative (`../resume/` etc.); the current page is marked
    `aria-current="page"`.
  - `docs/blog/` — the "Technical Ramblings" blog: `index.html` (post listing),
    one static `<slug>.html` per post, a shared `style.css`, and `images/`
    (post images). These posts were recovered from the Internet Archive's
    capture of the old Squarespace site at `tchien.com` (the Squarespace/
    WordPress XML export and the browser page-saves both came back as empty JS
    shells). Source of truth for the recovery was the archived RSS feed. Posts
    are plain static HTML now — edit them directly.
    - **Theme:** the blog deliberately does NOT use the terminal theme. It
      reproduces the old Squarespace (Brine/Clarkson) look — black background,
      white serif body (Minion Pro → Georgia stack), green Futura-PT-style
      headings, site title "Computer Systems Enthusiast" — since it's an
      archived copy of the old site. Colors/metrics came from the archived
      compiled site CSS. The rest of the site keeps the terminal theme.
  - `docs/CNAME` — custom-domain config for Pages (`www.taypc6.com`). Must live
    alongside the published content, i.e. inside `docs/`.
- `README.md`, `AGENT.md` — repo docs. **Not** part of the published site; keep
  them at the repo root, out of `docs/`.

## Conventions

- **Theme:** terminal / retro — green-on-black, monospace, mock-terminal window
  with command-prompt section headers. Keep new content in that idiom.
- **Self-contained:** no CDNs, external fonts, or JS frameworks. Shared,
  same-origin assets like `terminal.css` are fine (they work offline); just
  keep everything local. Inline the small bits of per-page JS. The page must
  load and work offline.
- **Accessibility:** respect `prefers-reduced-motion` (disable the cursor blink,
  scanlines, and smooth scroll under it).
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
