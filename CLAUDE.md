# CLAUDE.md

## Project overview

Personal blog/portfolio built with Hugo and the PaperMod theme. Hosted on Cloudflare Pages. Content is markdown files in a git repo, updated roughly monthly.

## Structure

- `hugo.toml` — site config (theme, menus, params, social links)
- `content/posts/` — blog posts (learning notes, debugging writeups, TILs)
- `content/projects/` — project pages (homelab, tools, side projects)
- `content/search.md` — PaperMod search page
- `archetypes/` — templates for `hugo new posts/...` and `hugo new projects/...`
- `layouts/index.html` — custom homepage (wordmark, featured post, post grid)
- `layouts/partials/header.html` — custom header (wordmark in nav, toggle far right)
- `layouts/partials/extend_head.html` — extra head tags (favicons, Google Fonts)
- `layouts/` — all other overrides go here, not in themes/
- `static/images/wordmark-dark.png` — wordmark for dark backgrounds (light coloured)
- `static/images/wordmark-light.png` — wordmark for light backgrounds (dark coloured)
- `static/images/posts/` — post cover images
- `assets/css/extended/custom.css` — CSS overrides (font, homepage layout, nav)
- `themes/PaperMod/` — theme (git submodule, don't edit directly)

## Commands

```bash
hugo server -D          # local dev server (includes drafts)
hugo server             # local dev server (published only)
hugo --minify           # production build to public/
hugo new posts/foo.md   # new blog post from archetype
hugo new projects/foo.md # new project page from archetype
```

## Content conventions

- Posts use frontmatter: title, date, draft, tags, description
- Projects add: repo (github URL), status (active | archived | wip)
- Set `draft: false` when ready to publish
- Tags are lowercase, hyphenated (e.g. `self-hosting`, `aws-bedrock`)
- Filenames are lowercase kebab-case
- Featured post: add `featured: true` to frontmatter; falls back to most recent post
- Post cover image: add `cover: { image: "/images/posts/foo.png", relative: false }` to frontmatter

## Design intent

- Minimal, clean developer aesthetic — not flashy
- Dark theme default (`defaultTheme = "dark"` in hugo.toml)
- Dracula syntax highlighting
- Lora serif font (Google Fonts, 400/500 weight)
- Two content sections: posts (learning/writing) and projects (things I've built)
- Homepage: tagline + social icons, featured post card with image, post grid below
- Wordmark in navbar (not text); two variants for light/dark mode

## Deployment

Cloudflare Pages auto-deploys on push to main.
- Build command: `hugo --minify`
- Build output: `public`
- Env var: `HUGO_VERSION = 0.145.0`

## PaperMod internals (useful for overrides)

- Dark mode: `html[data-theme="dark"]` / `html[data-theme="light"]` — set on `<html>` in baseof.html, NOT `body.dark`
- `defaultTheme = "dark"` renders `<html data-theme="dark">` directly in markup; JS only sets `"light"` if user toggles
- Nav layout: `.nav { display: flex; justify-content: space-between; }` with `.logo` and `#menu` as flex children
- Toggle lives in `.logo-switches` div; keep it there for correct alignment
- Custom CSS goes in `assets/css/extended/` — loaded after PaperMod core CSS
- Hugo is not installed locally — deploy via git push to trigger Cloudflare Pages build

## Things to avoid

- Don't edit files inside `themes/PaperMod/` — override in `layouts/` instead
- Don't use `body.dark` as a CSS selector — PaperMod uses `html[data-theme]`
- Don't put `#theme-toggle` inside `#menu` — it breaks alignment; keep in `.logo-switches`
- Don't use non-standard frontmatter keys unless necessary
