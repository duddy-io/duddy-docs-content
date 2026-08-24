# duddy-docs-content

The documentation source for [docs.duddy.io](https://docs.duddy.io).

This repository is Markdown (MDX), nothing else — no code, no build, no
dependencies. The site that renders it lives in the `duddy-docs` repository.

## Layout

```
docs/home/index.mdx                    →  https://docs.duddy.io/
docs/home/ai/models.mdx                →  https://docs.duddy.io/ai/models
docs/guides/overview.mdx               →  https://docs.duddy.io/guides/overview
docs/components/design/image.mdx       →  https://docs.duddy.io/components/design/image
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
else. `menu.json` is each section's entire sidebar and is validated on load;
a malformed one takes that whole section down.

## Publishing

The site serves a copy of this content bundled with the renderer, so a change
merged here appears on docs.duddy.io when the site is next deployed.

## Before you push

This repository is public. Anything committed is world-readable immediately
and stays in the history afterwards — no secrets, internal URLs, customer
names or unreleased features, including inside screenshots.

Nothing here is checked by CI: bad frontmatter, a malformed `menu.json` or a
link to a file that does not exist will publish cleanly and break in the
reader's browser.
