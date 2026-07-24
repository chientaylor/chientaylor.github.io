# AGENT.md

Guidance for AI agents (and humans) working in this repository.

## What this is

Personal website for Taylor Chien, served via **GitHub Pages** at the custom
domain **`www.taypc6.com`**. It is a static site with **no build step**.

## Layout

- `docs/` — the published site. GitHub Pages is configured to serve from this
  folder on the `main` branch.
  - `docs/index.html` — the entire site (single, self-contained file: HTML, CSS,
    and a few lines of JS inline; no external dependencies).
  - `docs/CNAME` — custom-domain config for Pages (`www.taypc6.com`). Must live
    alongside the published content, i.e. inside `docs/`.
- `README.md`, `AGENT.md` — repo docs. **Not** part of the published site; keep
  them at the repo root, out of `docs/`.

## Conventions

- **Theme:** terminal / retro — green-on-black, monospace, mock-terminal window
  with command-prompt section headers. Keep new content in that idiom.
- **Self-contained:** no CDNs, external fonts, or JS frameworks. Inline any CSS
  or JS. The page must load and work offline.
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
