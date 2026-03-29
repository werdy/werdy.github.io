---
title: "How to write blog posts for werdy.github.io"
description: "Guidelines and examples for creating markdown posts compatible with the Astro-Yi based werdy.github.io site"
date: 2026-03-29
---

# Blog Post Authoring Guide (werdy.github.io)

This document explains how to create new blog posts for the werdy.github.io site (Astro Yi theme). Place new files under `src/content/blog/` (or a subfolder) as `.md` or `.mdx` files. After committing and pushing, GitHub Actions will build and publish the site.

---

## Filename and location

- Put posts in: `src/content/blog/`
- Use a descriptive filename, e.g. `2026-03-29-new-feature.md` or `my-topic.md`.
- Files may be `.md` or `.mdx` (see examples in repo).

## Frontmatter (YAML)

At the top of each file include a YAML frontmatter block with metadata. Common fields used in existing posts:

- `title` (string) — required. The post title.
- `description` (string) — short summary shown in cards and meta description.
- `date` (YYYY-MM-DD) — required. Publication/creation date.
- `tags` (array) — example: `tags: [astro, feature]`.
- `category` (array or string) — optional grouping, used by theme (e.g. `category: [astro, feature]`).
- `mermaid: true` — enable Mermaid diagrams on the page (optional).
- `mathjax: true` — enable MathJax rendering (optional).
- `ogImage` — full URL to OpenGraph image (optional).
- `title`/`description`/`date` should be present for best compatibility.

Example frontmatter:

```yaml
---
title: "My new post"
description: "Short summary of the post"
date: 2026-03-29
tags: [guide, astro]
mermaid: true
mathjax: true
---
```

## Content features supported

The site (Astro Yi theme) supports many Markdown/MDX features. Use these patterns when authoring:

- Headings: `#`, `##`, `###` etc.
- Horizontal rules: `---`
- Emphasis: `**bold**`, `_italic_`, `~~strikethrough~~`
- Blockquotes: `> quote`
- Lists: `-`, `*`, `+` for unordered; numbers for ordered
- Code blocks: triple-fenced with language for syntax highlighting:

```js
```js
console.log('hello world')
```
```

- Code block titles and expressive-code markers (see examples in repo).

- Images: standard Markdown `![alt](url)` or use repo-hosted images. For large images consider hosting on a CDN and using absolute URL.

- Links: standard Markdown links `[text](url)`.

## Astro-Yi specific features/examples

The theme enables several custom shortcodes and features — examples from existing posts:

- Buttons

```text
:btn[Google]{href="https://www.google.com"}
```

- GitHub card

```text
::github{repo="owner/repo"}
```

- Collapse blocks

```text
:::collapse
Hidden content
:::
```

- Admonitions (tip/note/caution/danger)

```markdown
:::tip[Title]
Helpful tip text
:::
```

- Mermaid diagrams: set `mermaid: true` in frontmatter and include a ```mermaid fenced block.
- MathJax: set `mathjax: true` in frontmatter and use `$ ... $` or `$$ ... $$` for inline/block math.

## Comments (Giscus)

If you use the built-in comment support (Giscus), configure `src/consts.ts` per the repo examples and generate the script from https://giscus.app/. The post itself does not need extra markup — theme will connect pages to discussions via mapping (pathname).

## Images and assets

- Place local images in `public/` or host externally. Use absolute URLs for public CDN-hosted images to avoid broken links.
- If you add images to the repo, commit them under `public/` or a dedicated `assets/` path and reference them by `/assets/...` or `/public/...` path.

## MDX notes

- `.mdx` files may include JSX components. Keep component usage minimal and ensure components are available in the theme.
- If you use MDX, ensure exported components or imports are valid in the site build context.

## Commit & publish workflow

1. Create the new `.md` or `.mdx` file under `src/content/blog/`.
2. Commit with a clear message, e.g. `git add src/content/blog/2026-03-29-my-post.md && git commit -m "Add: my-post"`.
3. Push to `main` (or the branch configured for Pages). GitHub Actions will run and publish to GitHub Pages automatically if configured.

## Examples in this repo

See existing posts in this folder for patterns:
- `250227-astro-yi-theme-setup.md` — shows setup steps and images.
- `markdown-elements.md` — demonstrates markdown capabilities.
- `new-features.md` — shows mermaid, mathjax, admonitions, and expressive code usage.

## Checklist before publishing

- [ ] Title, description, date present in frontmatter
- [ ] Tags and category as needed
- [ ] Images referenced with correct path or hosted URL
- [ ] If using mermaid/mathjax, enable in frontmatter
- [ ] Run `pnpm build` (or `npm run build`) locally to confirm no build errors

---

If you want, I can:
- Create a pull request template or CONTRIBUTING.md that includes this guide.
- Add a small script to create a new post with frontmatter pre-filled.
- Automatically commit & push this file to the repository (I can do that now).

