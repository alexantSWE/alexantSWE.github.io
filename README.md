# alexant — personal intro site

A small bilingual (Persian/English) personal introduction site built with
[Hugo](https://gohugo.io) using a **hand-written theme** (`themes/handyman`).

- Persian is the default language and renders at `/` with `dir="rtl"`.
- English lives at `/en/`.
- Everything is static and tracker-free. A tiny inline script remembers the
  visitor's light/dark choice and opens the mobile menu.

## Requirements

- Hugo **Extended** ≥ 0.167 (installed via scoop: `scoop install hugo-extended`)

## Local development

```bash
hugo server --port 1313
```

Open http://localhost:1313 (Persian) and http://localhost:1313/en/ (English).

## Build

```bash
hugo --minify
```

Output goes to `public/`.

## Project layout

```
hugo.toml              multilingual config (fa default + rtl, en + ltr), menus, params
content/fa/            Persian content  (served at /)
content/en/            English content  (served at /en/)
i18n/                  UI strings per language (fa.toml, en.toml)
assets/css/main.css    single stylesheet using CSS logical properties
static/                fonts, favicon.svg, og.png (sharing card)
layouts/robots.txt     robots.txt with the sitemap URL
.github/workflows/     GitHub Pages build & deploy
themes/handyman/
  layouts/_default/    baseof.html, list.html, single.html
  layouts/index.html   home page
  layouts/partials/    head, header, footer, lang-switch, notes-list
```

### How RTL works

There is only one stylesheet. It uses **logical properties** (`inline-start`,
`inline-end`, `padding-inline`, `border-inline`) instead of `left`/`right`.
Hugo sets `dir="rtl"` on `<html>` from `languages.fa.direction`, and the browser
flips every measurement automatically. Code blocks are forced back to LTR with
`direction: ltr`.

### Adding content

```bash
hugo new content fa/notes/my-note.md
hugo new content en/notes/my-note.md
```

Give both files the same `translationKey` in front matter so the language
switch links them together. Keep `draft: true` until you're ready.

To add a repo to the home page, append to `[[params.repos]]` in `hugo.toml`.

### Social previews

`static/og.png` is the 1200×630 image shown when a link is shared (for example
on Telegram). Replace it with a fresh screenshot or card whenever the design
changes; `static/favicon.svg` is the browser tab icon.

## Deploy — GitHub Pages

This repository is set up as a **user site**, so it must be named
`alexantSWE.github.io` and is published at https://alexantSWE.github.io/.

`baseURL` in `hugo.toml` is already set to that address, and
`.github/workflows/hugo.yml` builds and deploys on every push to `main`.

**One-time setup:**

1. On GitHub, create a **public** repository named `alexantSWE.github.io`.
2. Push this project to it (see below).
3. In the repository: **Settings → Pages → Build and deployment → Source =
   GitHub Actions**.
4. Push to `main` (or run the workflow manually from the **Actions** tab) and
   wait for it to finish.

**Pushing an existing local copy:**

```bash
git remote add origin https://github.com/alexantSWE/alexantSWE.github.io.git
git push -u origin main
```

### Optional: custom domain

A custom domain is the most durable way to stay reachable if `github.io` is
ever filtered. After the site is live:

1. Add the domain under **Settings → Pages → Custom domain**.
2. Create `static/CNAME` containing just the domain (for example
   `alexant.example`), and set `baseURL` in `hugo.toml` to
   `https://alexant.example/`.
3. At your DNS provider, point the apex domain at GitHub Pages' A records
   (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`)
   and `www` at a CNAME to `alexantSWE.github.io`. Then enable **Enforce HTTPS**.

> The old Cloudflare Pages setup (`wrangler.toml`) has been removed. Cloudflare
> Pages still works fine as a fallback, but its `*.pages.dev` address is
> filtered in some networks, which is why the site moved here.
