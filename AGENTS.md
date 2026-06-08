# PackClaw Web — AGENTS.md

## What this repo is

Static marketing and documentation site for PackClaw (an OpenClaw installer). No build toolchain, no package manager, no JS framework. Pure HTML + CSS + minimal inline JavaScript.

## Structure

- `index.html` — Landing page (self-contained: CSS in `<style>`, JS in `<script>`)
- `style.css` — Shared stylesheet used by `docs/` pages (landing page has its own inline styles)
- `docs/` — Tutorial sub-site, links back to root
  - `docs/index.html` — Tutorial hub
  - `docs/tutorials/*.html` — Individual tutorials (feishu, wecom, dingtalk, qq, wechat, uninstall)
  - `docs/assets/` — Tutorial screenshots (hashed filenames via Vite build from upstream)
- `releases/` — Changelog page + electron-builder yml files (`latest.yml`, `latest-mac.yml`, etc.)
- `models/51key-model-options.json` — Model list consumed by the PackClaw desktop app
- `assets/` — Site images (favicon etc.)

## Key conventions

- **No build step.** Edit HTML/CSS directly, preview by opening files in a browser.
- **Two separate style systems:** Landing page (`index.html`) uses inline `<style>` with its own CSS variables (`--bg`, `--accent`, etc.). `docs/` pages import `style.css` which uses a different set of variables (`--bg-deep`, `--coral-bright`, etc.). Keep them consistent where they overlap but do not assume they share the same token names.
- **Language:** All user-facing text is in simplified Chinese (`lang="zh-CN"`).
- **Cross-linking:** `docs/` pages link to `../index.html` and `../style.css` (relative paths). `index.html` nav links to `docs/index.html`.
- **Download links** in `index.html` point to `releases/` paths — these are not present in the repo; they are served externally or from a different deployment step.

## Editing tips

- When adding a new tutorial page, follow the pattern in existing `docs/tutorials/*.html` files.
- Tutorial images go in `docs/assets/` with content-hashed filenames.
- The `releases/` yml files (`latest.yml`, `latest-mac.yml`, `dev.yml`, `dev-mac.yml`) are electron-builder auto-update manifests — update version strings there when cutting a new release.
- The landing page and docs sub-site have **different** nav headers and footers — edit them independently.
