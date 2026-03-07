# Blog Setup

## Quick start

```bash
# 1. Install Hugo (https://gohugo.io/installation/)
brew install hugo  # macOS

# 2. Clone this repo (or init fresh and copy these files in)
cd blog

# 3. Add PaperMod theme
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod

# 4. Run locally
hugo server -D  # -D includes drafts

# 5. Open http://localhost:1313
```

## Writing a new post

```bash
hugo new posts/my-new-post.md
```

Edit the file in `content/posts/`, set `draft: false` when ready.

## Writing a new project page

```bash
hugo new projects/my-project.md
```

## Deploy to Cloudflare Pages

1. Push repo to GitHub
2. In Cloudflare Pages dashboard: connect repo
3. Build command: `hugo --minify`
4. Build output: `public`
5. Set env var: `HUGO_VERSION = 0.145.0`
6. Done — auto-deploys on push to main

## Theme switching

```bash
# Remove current theme
git rm themes/PaperMod

# Add new one
git submodule add https://github.com/whoever/new-theme.git themes/NewTheme
```

Update `theme = "NewTheme"` in `hugo.toml` and adjust config keys to match.
Stick to standard frontmatter (title, date, tags, draft, description) to stay portable.

## Directory structure

```
blog/
├── hugo.toml              # site config
├── archetypes/
│   ├── posts.md           # template for new posts
│   └── projects.md        # template for new projects
├── content/
│   ├── posts/             # blog posts
│   ├── projects/          # project writeups
│   └── search.md          # search page
├── layouts/               # custom layout overrides (empty for now)
├── static/                # images, favicons, etc.
└── themes/
    └── PaperMod/          # added via git submodule
```
