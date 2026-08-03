# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal wiki for a datamatiker (computer science) student's coursework notes: a set of
static, standalone HTML pages with no build step, no package manager, and no server-side code. It's
published via GitHub Pages at https://deni5-student.github.io/learning2csharp/. Content and
conversation with the user should be in Danish (`lang="da"`).

## Development

There is no build/lint/test tooling — just edit the HTML files directly and open them in a browser
(or refresh the GitHub Pages URL) to see changes. Changes are committed and pushed directly to `main`
(no CI, no PR review) — GitHub Pages redeploys automatically within seconds of a push.

## Architecture

Every top-level page is a fully self-contained HTML document with its own `<style>` block — there is
no shared CSS file, JS module, or template system. All pages share this structure:

- A `.wiki-container` CSS grid splitting the page into a fixed 260px `<aside class="sidebar">` and a
  centered, max-width `<main class="content">` area (`max-width: 1100px; margin: 0 auto;`).
- The sidebar markup (Navigation / Vidensbase / Skole link groups) is duplicated verbatim across
  **every** page. **When adding, renaming, or reordering a page, update the sidebar `<ul>` in every
  HTML file, not just one.** The active page's link is highlighted via an inline
  `style="background: #f0f4f8; color: #0066cc; font-weight: bold;"` on its `<a>` — this must be
  moved to match the current page, and removed from the others.
- Some topics have sub-pages, shown as an indented link directly under their parent in the sidebar
  using `class="sub-link"` (defined as `.sidebar a.sub-link { padding-left: 28px; font-size: 0.9rem;
  color: #718096; }`) with a `↳` prefix in the link text — e.g. Visual Studio/JetBrains Rider under
  C# Learning, and WSL under Windows. This is a plain always-visible indented list, not a
  collapsible/JS-driven menu.
- Reusable content-area patterns duplicated across pages as needed: `.callout` (tip box),
  `.grid-links`/`.card` (shortcut cards), `.command-list` (concept/command reference lists), `pre` /
  `pre code` (VS-style code blocks), `.post`/`.post-date` (blog-style entries on Opdateringer.html).

Because every page duplicates the same `<style>` block with minor variations, when changing shared
visual style (sidebar colors, fonts, grid layout, etc.) expect to replicate the edit across all HTML
files individually rather than editing one shared source.

### Current Vidensbase order

`CSharp.html` (with `VisualStudio.html` and `Rider.html` as sub-links) → `HTML-Guides.html` →
`CSS-Styling.html` → `Ubuntu.html` → `Python.html` → `Windows.html` (with `WSL.html` as a sub-link).

### Opdateringer.html

Blog-style changelog (renamed from "Daglige Notater" since updates don't happen daily). Newest post
goes at the top, directly under the callout tip box; older posts stay below it. Keep entries short
and factual — no references to what was learned at a job/employer (the user has asked this be kept
generic/neutral, since the site is public).

### Images

Screenshots and other images go in `billeder/` (see `billeder/README.md` for naming convention and
the `.screenshot` CSS snippet to reuse). Not yet used on any page as of this writing.
