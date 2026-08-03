# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a personal C# learning wiki: a set of static, standalone HTML pages with no build step,
no package manager, and no server-side code. It's published via GitHub Pages at
https://deni5-student.github.io/learning2csharp/. Content and notes are in Danish (`lang="da"`).

## Development

There is no build/lint/test tooling — just edit the HTML files directly and open them in a browser
(or refresh the GitHub Pages URl) to see changes.

## Architecture

Each top-level page (`index.html`, `HTML-Guides.html`, `CSS-Styling.html`, `Retningslinjer.html`,
`Daglige-Notater.html`, `Projekter.html`) is a fully self-contained HTML document with its own
`<style>` block — there is no shared CSS file, JS module, or template system. The pages share a
common structure:

- A `.wiki-container` CSS grid splitting the page into a fixed 260px `<aside class="sidebar">` and
  a `<main class="content">` area.
- The sidebar markup (Navigation / Vidensbase / Personligt link groups) is duplicated verbatim
  across every page. **When adding, renaming, or reordering a page, update the sidebar `<ul>` in
  every HTML file, not just one.** The active page's link is highlighted via an inline
  `style="background: #f0f4f8; color: #0066cc; font-weight: bold;"` on its `<a>` — this must be
  moved to match the current page, and removed from the others.
- `HTML-Guides.html` is the only page pulling external resources: highlight.js (via cdnjs) for
  syntax-highlighting embedded C# code samples inside `<pre><code class="language-csharp">` blocks,
  activated with `hljs.highlightAll()`.
- `CSS-Styling.html` additionally demonstrates a flex-based `.content` layout with an `.edit-zone` /
  `.btn-edit` "Edit this page on GitHub" call-to-action pinned to the bottom of the content area.

Because every page duplicates the same `<style>` block with minor variations, when changing shared
visual style (sidebar colors, fonts, grid layout, etc.) expect to replicate the edit across all HTML
files individually rather than editing one shared source.
