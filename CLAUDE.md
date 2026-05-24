# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with
code in this repository.

## Development Commands

```bash
# Install dependencies
bundle install

# Serve locally (http://localhost:4000)
bundle exec jekyll serve

# Serve with incremental builds
bundle exec jekyll serve --incremental

# Include future-dated posts
bundle exec jekyll serve --future true --incremental
```

The `JEKYLL_GITHUB_TOKEN` environment variable (personal access token with
`public_repo` scope) is required for the jekyll-github-metadata plugin, which
powers the "Suggest an edit" links on posts.

## Branch & PR Workflow

**Never commit directly to `main`.** All changes must go through a branch
and pull request:

```bash
git checkout -b my-branch-name
# make changes
git add <files>
git commit -m "descriptive message"
git push -u origin my-branch-name
# then open a PR targeting main
```

Assign PRs to @w0ger for review.

## Linting & Spell Check

GitHub Actions runs these on push/PR to main. To run locally:

```bash
markdownlint _posts
cspell _posts/**/*.md
```

### Markdownlint Rules (`.markdownlint.json`)

- Line length: **80 characters** (not enforced in code blocks, tables, or
  headings)
- MD033 (inline HTML): disabled — HTML is allowed
- MD041 (first-line heading): disabled
- MD026 (trailing punctuation in headings): disabled
- MD014 (dollar signs before commands): disabled
- MD031 (fenced code blocks around lists): disabled
- MD036 (emphasis as heading): disabled

### cSpell Custom Words

Technical terms, proper nouns, and domain-specific words live in `cSpell.json`
under the `words` array. Add new words there when the spell checker flags
legitimate content.

```bash
# Check a specific file
cspell --config ./cSpell.json --no-progress "path/to/file.md"
```

## Architecture

This is a **Jekyll personal blog** using the
[Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) remote theme
(`mmistakes/minimal-mistakes@4.26.2`, skin: `air`), hosted on GitHub Pages at
rogernoden.com.

### Content

- **Posts**: `_posts/YYYY-MM-DD-slug.md` — standard Jekyll date-prefixed
  convention
- **Pages**: `_pages/` — static pages (home, about, posts, projects,
  categories, tags)
- **Projects**: `_projects/` — a Jekyll collection with its own permalink
  structure

### Post Frontmatter

All posts use this frontmatter template. Fields marked with `*` are required:

```yaml
---
title: "Post Title Here"          # *
comments: true                    # * always true for posts
tags:
  - Tag One
  - Tag Two
date: 2026-04-21 00:00:00.000000000 -05:00   # * include timezone offset
excerpt: >-
  A one-to-two sentence summary shown in post listings. Can wrap
  across lines using YAML block scalar syntax.
header:
  teaser: images/filename.jpg     # relative to site root, no leading slash
  overlay_image: images/filename.jpg
  overlay_filter: 0.5             # typically 0.5 for readability
  caption: >-
    Photo by [**Photographer Name**](https://unsplash.com/@handle)
    on [**Unsplash**](https://unsplash.com/photos/photo-slug)
categories:
  - Technology                    # broad; see existing posts for conventions
  - Development
---
```

`layout: single` and `classes: wide` are set globally in `_config.yml`
defaults — do not repeat them in post frontmatter.

`read_time: true`, `related: true`, `show_date: true`, and `author_profile:
true` are also set globally and should be omitted from individual posts.

### Project Frontmatter

Projects differ from posts — no date, no comments, and external image URLs
are supported:

```yaml
---
title: Project Name
layout: single
excerpt: Brief description &mdash; HTML entities are fine here.
header:
  teaser: https://external-url.com/image.png
  overlay_image: https://external-url.com/project-header.png
---
```

`comments: false` and no `read_time` are set globally for projects in
`_config.yml`.

### Pages

Static pages in `_pages/` use layout-specific frontmatter:

| Layout | Used for | Notes |
|--------|----------|-------|
| `splash` | Home page | Uses `feature_row` for grid sections |
| `posts` | Blog index | Minimal frontmatter; posts auto-populated |
| `collection` | Projects index | `entries_layout: grid` for card view |
| `tags` | Tags archive | Auto-populated by Jekyll |
| `categories` | Categories archive | Auto-populated by Jekyll |
| `single` | About, other pages | Standard single-column layout |

### Image Conventions

- Store images in `/images/` at the repo root — **not** `/assets/images/`
- Reference them without a leading slash: `images/filename.jpg`
- Use the VS Code `pimg` snippet (see below) for inline post images:
  `![alt text]({{site.post-images}}/filename.jpg)`
- For header images from Unsplash, include full attribution in the `caption`
  field using bold-linked photographer name and Unsplash URL

### Theme Customization

The site overrides specific Minimal Mistakes components rather than forking
the theme:

- `_layouts/single.html` — overrides the theme's single post layout to inject
  the custom metadata include
- `_includes/post__meta__witheditlinks.html` — replaces the theme's post
  metadata block; adds "Suggest an edit" and "Issue? Question?" links that
  auto-generate GitHub URLs from `site.repository` and `page.path`
- `_includes/page__hero.html` — custom hero image section
- `_includes/head/custom.html` — favicon links (`<head>` additions)
- `_sass/custom.scss` — minimal SCSS overrides (footer spacing, page meta
  padding)

### Configuration

`_config.yml` is the primary configuration file. Key sections:

- **Giscus comments**: configured with repo ID and category ID — update these
  if the GitHub repo changes
- **Author profile**: social links (BlueSky, Mastodon, GitHub, IMDb,
  LinkedIn, Letterboxd), bio, avatar path
- **Defaults**: posts use `single` layout with author profile, comments, read
  time, and related posts enabled; projects disable comments and read time
- **Archives**: liquid-type archives for categories and tags
- **Permalink**: `/:year/:month/:title/`
- **Markdown**: kramdown with GFM

### Navigation

`_data/navigation.yml` controls the top nav links (Blog, Projects, About).
`_data/ui-text.yml` contains multilingual UI strings for 30+ languages —
rarely needs editing.

### VS Code Setup

`.vscode/blog-snippets.code-snippets` defines a `pimg` snippet for Markdown
files. Type `pimg` and press Tab to expand:

```markdown
![alt text]({{site.post-images}}/filename.jpg)
```

`.vscode/settings.json` configures markdownlint to match the project's
`.markdownlint.json` rules (H1 and trailing-punctuation rules disabled).

## GitHub Actions

`.github/workflows/housekeeping.yml` runs on every push or PR to `main`:

| Job | Tool | Target |
|-----|------|--------|
| Markdown linting | `avtodev/markdown-lint:v1` (Docker) | `_**/*.md` |
| Spell checking | cSpell via Node.js 18 | `**/*.md` |

Both jobs must pass before merging. Run them locally (see Linting section)
before pushing to avoid CI failures.

Dependabot is configured (`.github/dependabot.yml`) to keep GitHub Actions
dependencies up to date.
