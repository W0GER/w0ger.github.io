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

## Linting & Spell Check

GitHub Actions runs these on push/PR to main. To run locally:

```bash
markdownlint _posts
cspell _posts/**/*.md
```

Custom words for cSpell are in `cSpell.json`.

## Architecture

This is a **Jekyll personal blog** using the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)
remote theme (`mmistakes/minimal-mistakes@4.26.2`, skin: `air`), hosted on
GitHub Pages at rogernoden.com.

### Content

- **Posts**: `_posts/YYYY-MM-DD-slug.md` — standard Jekyll date-prefixed
  convention
- **Pages**: `_pages/` — static pages (home, about, posts, projects, categories,
  tags)
- **Projects**: `_projects/` — a Jekyll collection with its own permalink
  structure

### Theme Customization

The site overrides specific Minimal Mistakes components rather than forking the
theme:

- `_layouts/single.html` — overrides the theme's single post layout to inject
  the custom metadata include
- `_includes/post__meta__witheditlinks.html` — replaces the theme's post metadata
  block; adds "Suggest an edit" and "Issue? Question?" links that auto-generate
  GitHub URLs from `site.repository` and `page.path`
- `_includes/page__hero.html` — custom hero image section
- `_includes/head/custom.html` — custom `<head>` additions
- `_sass/custom.scss` — minimal SCSS overrides (footer spacing, page meta
  padding)

### Configuration

`_config.yml` is the primary configuration file. Key sections:

- **Giscus comments**: configured with repo ID and category ID — update these if
  the GitHub repo changes
- **Author profile**: social links, bio, avatar path
- **Defaults**: posts use `single` layout with author profile, comments, read
  time, and related posts enabled
- **Archives**: liquid-type archives for categories and tags

### Navigation

`_data/navigation.yml` controls the top nav links.
