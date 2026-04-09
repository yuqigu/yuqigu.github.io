# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Yuqi Gu's academic personal website, built on the [al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. Hosted at `yuqigu.github.io`. The `source` branch contains the editable content; deployment builds go to a separate branch.

## Build and serve

```bash
# Install dependencies (first time)
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Build static site
bundle exec jekyll build
```

The site builds to `_site/`. The `_site.zip` is a pre-built static export.

## Architecture

### Content files (what you'll edit most)

- `_pages/about.md` — Homepage with bio, research interests, and CV link
- `_pages/publications.md` — Research page; uses `{% bibliography %}` Liquid tags to render from `_bibliography/papers.bib`
- `_pages/teaching.md`, `_pages/news_arc.md` — Other nav pages
- `_news/*.md` — Individual news items (one file per item); shown on homepage up to `news_limit: 10` in `_config.yml`
- `_bibliography/papers.bib` — All publications and preprints as BibTeX

### Bibliography system (jekyll-scholar)

Publications are rendered via the `jekyll-scholar` plugin. Key fields used beyond standard BibTeX:

- `pubtype`: `preprint` or `pub` — controls which section a paper appears in on the publications page
- `arxiv`: arXiv ID — renders an arXiv link
- `journalurl`: — renders a Journal link
- `pdf`: filename in `assets/pdf/` — renders a PDF link
- `award`: text string — displayed as an award note under the entry
- `abbr`: venue abbreviation — looked up in `_data/venues.yml` for a linked badge

The bibliography template is `_layouts/bib.html`. Author formatting rules are hardcoded there:
- "Yuqi" is italicized (site owner)
- Students/postdocs under supervision (Wenjin, Seunghyun, Ling, Chengzhu, Zhongyuan, Jia, Zhiyu) are underlined
- Other coauthors with entries in `_data/coauthors.yml` get hyperlinked names

### News items

Each file in `_news/` has front matter:
```yaml
---
layout: post
date: YYYY-MM-DD
inline: true
---
News text here (Markdown, can include links).
```

The homepage shows the 10 most recent (controlled by `news_limit` in `_config.yml`).

### Configuration

- `_config.yml` — Main site config (personal info, plugins, scholar settings, feature flags)
- `_config_github.yml` — Alternate config for GitHub Pages deployment
- `_data/coauthors.yml` — Maps author last names to URLs for hyperlinking in the bib template

### Assets

- `assets/pdf/` — PDFs served directly (CV versions, paper slides, etc.)
- `assets/img/` — Images including `prof_pic.jpg`

## Common tasks

**Add a news item:** Create `_news/<shortname>.md` with front matter above.

**Add/update a paper:** Edit `_bibliography/papers.bib`. Use `pubtype=preprint` or `pubtype=pub`. Place PDFs in `assets/pdf/` and reference by filename in the `pdf` field.

**Update the CV link:** Edit the PDF filename in `_pages/about.md` (the `relative_url` filter line near the bottom).

**Add a supervised student to underline in bib:** Add their first name to the hardcoded list in `_layouts/bib.html` (lines ~32 and ~46).

**Add a coauthor hyperlink:** Add an entry to `_data/coauthors.yml` with their last name, first name variants, and URL.
