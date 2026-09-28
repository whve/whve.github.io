# Agent Guide

This file is for AI agents and automated maintainers. `README.md` is for human users and explains how to use the site.

## Project purpose

This repository is a Quarto website named Personal Knowledge Base. It organizes English and Chinese notes into four sections:

- `projects/`: active work and time-bound efforts.
- `areas/`: ongoing responsibilities and topics of attention.
- `resources/`: reusable references, notes, and collections.
- `archives/`: completed work and historical reviews.

## Source and generated files

- Edit `.qmd`, `.md`, `_quarto.yml`, `styles.css`, workflow files, and documentation in the project root.
- `docs/` is generated output. Do not edit files there by hand.
- Run `quarto render` after source changes. The generated site is written to `docs/`.
- Do not add generated files to source content listings.

## Article convention

Articles do not require a language suffix. Any `.md` or `.qmd` file placed in a content section is included in its listing. New articles should use this front matter:

```yaml
---
title: "Clear article title"
date: YYYY-MM-DD
categories: [category]
description: "One concise sentence describing the article."
---
```

Use `categories`, not `tags`, for listing filters. Keep descriptions useful to both human readers and agents. This site intentionally has no cover images, thumbnails, or image placeholders.

## Navigation

`articles.qmd` is the complete cross-section index. It uses a date-descending table listing with filtering, sorting, and categories. Do not add random-article or previous/next navigation without an explicit decision about ordering and maintenance cost.

## Maintenance operations

- Create: add a `.md` or `.qmd` file to the appropriate content section with the required front matter.
- Read: use `articles.qmd`, a section listing, site search, or `quarto preview`.
- Update: edit the source article, then render the site and check affected links.
- Delete: remove the source article and render again; never delete only its generated page in `docs/`.
- Archive: move completed material to `archives/`, update its categories if needed, and check internal links.
- Rename: check source links, generated URLs, and external bookmarks before and after renaming.

## Validation

Run these commands after changes:

```bash
quarto check
quarto render
```

Then check that the generated pages contain the expected article links and that no old theme terms, image configuration, or broken internal links remain.

## Change boundaries

Prefer small, focused changes. Preserve existing article meaning unless the task explicitly asks for editorial rewriting. Do not directly edit `docs/` to fix a source problem.
