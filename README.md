# duddy-docs-content

The documentation source for **[docs.duddy.io](https://docs.duddy.io)**.

This repo is Markdown, nothing else — no code, no build, no dependencies. The
site that renders it lives in `duddy-docs` and fetches these files from `main`.

## Editing

```
docs/home/index.mdx                    →  https://docs.duddy.io/
docs/home/ai/models.mdx                →  https://docs.duddy.io/ai/models
docs/guides/overview.mdx               →  https://docs.duddy.io/guides/overview
docs/components/design/image.mdx       →  https://docs.duddy.io/components/design/image
docs/<section>/menu.json               →  that section's sidebar
```

Sections are `home`, `guides`, `components` and `changelogs`. `home` is served
at the root, so its files carry no `/home` prefix in the URL.

Every document opens with frontmatter:

```yaml
---
title: Create a project
description: One line, used as the page's meta description.
---
```

Push to `main` and the change appears on the site — no deploy step.

## Before you push

This repository is **public**. Anything committed is world-readable
immediately and stays in the history afterwards, so no secrets, internal URLs,
customer names or unreleased features — including inside screenshots.

Nothing here is checked by CI: bad frontmatter, a malformed `menu.json` or a
link to a file that does not exist will publish cleanly and break in the
reader's browser. See `AGENTS.md` for the full set of rules.
