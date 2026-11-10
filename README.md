# duddy-docs-content

The documentation source for [docs.duddy.io](https://docs.duddy.io).

This repository is Markdown (MDX), nothing else — no code, no build, no
dependencies. The site that renders it lives in the `duddy-docs` repository.

## Layout

```
docs/home/index.mdx                    →  https://docs.duddy.io/
docs/home/ai/models.mdx                →  https://docs.duddy.io/ai/models
docs/guides/overview.mdx               →  https://docs.duddy.io/guides/overview
docs/components/layout.mdx             →  https://docs.duddy.io/components/layout
docs/media/home/how-duddy-works.svg    →  https://docs.duddy.io/media/home/how-duddy-works.svg
docs/<section>/menu.json               →  that section's sidebar
```

Sections are `home`, `guides`, `components` and `changelogs`. `home` is
served at the root, so its files carry no `/home` prefix in the URL. A file
path is a public URL — renaming a document breaks every external link to it.

Every document opens with frontmatter, and unknown keys are rejected:

```yaml
---
title: Create a project
description: One line, used as the page's meta description.
---
```

MDX may use Markdown plus the components the renderer registers — nothing
else: `Callout`, `CodeBlock`, `Accordion`/`AccordionItem`, `YouTube`,
`NextPrev`, `Badge`, `Terminal`, `Card`/`CardGrid`, `Steps`/`Step`, `Figure`
and `FigureRow`. Any other tag is a render error in production. `menu.json`
is each section's entire sidebar (and its search index); a page that is in no
menu cannot be found, and a malformed menu takes the whole section down.

## Images

Pictures live under `docs/media/<section>/` and are linked as `/media/…`
(png, jpg, webp, avif, gif or svg, up to 5 MB). Alt text is required.

```mdx
![How Duddy works](/media/home/how-duddy-works.svg "Optional caption")

<Figure src="/media/guides/layout-containers.svg" dark="/media/guides/layout-containers.dark.svg"
  alt="Row, Column and Stack side by side" />
<Figure src="/media/apps/notes-blue-home.png" alt="A notes app's home screen" frame="phone" />
```

An image alone on its line becomes a figure. `dark` is swapped in for dark
themes and must be the same size; `frame="phone"` frames an app screenshot;
`<FigureRow>` puts two or three figures side by side.

## Style

Plain, second person, British spelling, sentence-case headings, UI labels in
**bold** exactly as the product shows them. Status words are exactly *beta*
and *coming soon*. Plan numbers live on one page (Plans and limits); other
pages link to it. Every page ends with short next steps.

## Publishing

The site serves a bundled copy, so a merged change appears on docs.duddy.io
when the site is next deployed.

## Before you push

This repository is public. Anything committed is world-readable immediately
and stays in the history afterwards — no secrets, internal URLs, customer
names or unreleased features, including inside screenshots.

Nothing here runs CI, so check with the renderer before you push. From a
`duddy-docs` checkout beside this one:

```sh
npm run docs:validate -- --root ../duddy-docs-content/docs
```

It checks frontmatter, renders every page with the real component set, and
checks every internal link, `#anchor`, `/media` file and menu entry. Exit 1 on
any error. Deploy the renderer before content that uses a new component.
