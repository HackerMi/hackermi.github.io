# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal blog ("HackerMi's Blog") built with Jekyll and hosted on GitHub Pages at `www.hackermi.com` (see `CNAME`). Content is written in Chinese and split into two categories — `tech` (产品 & 技术) and `life` (生活).

## Commands

Local development needs Ruby + Jekyll + the `jekyll-paginate` gem (there is no `Gemfile`):

```bash
jekyll serve   # build & serve at http://localhost:4000, auto-rebuilds on change
jekyll build   # one-off build into _site/ (git-ignored)
```

GitHub Pages builds and deploys automatically on push to `master`. The `_config.yml` key `gems: [jekyll-paginate]` is required for the pagination plugin both locally and on Pages.

## Architecture

Standard Jekyll layout, but note these specifics:

- **Category = subdirectory.** Posts live in `_posts/tech/` and `_posts/life/`, and their front matter sets `categories: tech` (or `life`). The category index pages (`tech/index.html`, `life/index.html`) filter on `site.categories.tech` / `site.categories.life`, so the directory and the front-matter category must match.
- **Pagination** (`jekyll-paginate`, 10 posts/page) is used only on the homepage `index.html` — Jekyll's paginator works on exactly one page. The homepage excerpt is split on the `<!--more-->` marker inside each post.
- **Permalinks** are `/:year-:month/:title/`; `_config.yml` sets `url: http://www.hackermi.com`, and several places (favicon, atom feed, analytics) rely on `site.url` / `site.feed` staying consistent.
- **Post front matter** expects `layout: post`, `title`, `categories` (`tech` or `life`), and `tags` (space-separated; each tag links to a `/tags#tag-ref` anchor).
- **Layouts** (`_layouts/`): `default.html` is the full-page shell (nav, css/js, google-code-prettify, analytics); `post.html` (article + prev/next pager + Disqus) and `page.html` (static pages) extend it; `blank.html` is an empty shell used only by `atom.xml`.
- **Post images** go in `assets/<topic>/` (e.g. `assets/carlink/`) and are referenced by relative path from the post markdown.
- **Drafts** live in `_drafts/` and are not published by GitHub Pages; `_drafts/MindMap/` holds PNG images.

## Writing a new post

1. Create `_posts/<tech|life>/YYYY-MM-DD-slug.md`.
2. Front matter: `layout: post`, `title`, `categories: tech` (or `life`), `tags: ...`.
3. Put `<!--more-->` after the intro paragraph to control the homepage excerpt.
