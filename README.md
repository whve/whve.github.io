# Personal Knowledge Base

This is a small Quarto website for reading and maintaining a searchable collection of notes. It is organized into four sections: Projects, Areas, Resources, and Archives.

`README.md` is for human users. `AGENTS.md` is for AI agents and automated maintainers; it contains the stricter repository rules.

## Start locally

Install [Quarto](https://quarto.org/) and run:

```bash
quarto preview
```

To build the static site without starting a server:

```bash
quarto render
```

The generated site is written to `docs/`. It is build output and should not be edited manually.

## Content structure

- `projects/`: active work and time-bound efforts.
- `areas/`: ongoing responsibilities and topics of attention.
- `resources/`: reusable references, notes, and collections.
- `archives/`: completed work and historical reviews.

`articles.qmd` is the complete cross-section index. It combines all Markdown and Quarto articles, sorts them by date, and provides filtering and sorting controls.

## Maintain articles

### Create

Create a Markdown or Quarto file in the appropriate directory. A language suffix is optional:

```yaml
---
title: "Clear article title"
date: 2026-09-24
categories: [topic]
description: "One concise sentence describing the article."
---
```

Use `categories` rather than `tags`. Cover images, thumbnails, and image placeholders are intentionally not part of this site.

### Read

Use `articles.qmd` for the complete index, a section page for one category, site search, or `quarto preview` for local reading.

### Update

Edit the source `.md` or `.qmd` file, then run `quarto render`. Do not edit the generated HTML in `docs/`.

### Delete

Delete the source article and run `quarto render` again. Removing only a generated file in `docs/` is temporary and will be undone by the next build.

### Archive

Move completed material to `archives/`, update its categories if needed, and check links that refer to the old location.

### Rename

Check internal links, generated URLs, and external bookmarks after renaming a file. Use a redirect strategy before changing a URL that may already be public.

## Publishing

The GitHub Actions workflow in `.github/workflows/publish.yml` renders the site and deploys the `docs/` artifact to GitHub Pages. The repository's Pages settings must use GitHub Actions as the deployment source.

## Workspace

Open `personal-knowledge-base.code-workspace` in VS Code.

## Maintenance rules

See `AGENTS.md` for source boundaries, metadata rules, navigation constraints, and validation requirements.
