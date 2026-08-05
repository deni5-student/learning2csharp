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
  `pre code` (VS-style code blocks), `.post`/`.post-date` (blog-style entries on Opdateringer.html),
  `.term`/`.term-heading`/`.term-en` (glossary entry cards on Fagord.html, pairing a Danish term with
  its English equivalent), `.reference` (amber citation box under a glossary entry, left intentionally
  blank with a placeholder like "kapitel ___, s. ___" — the user fills in real page numbers from their
  own physical textbook by hand; never invent a page/chapter number here).
Because every page duplicates the same `<style>` block with minor variations, when changing shared
visual style (sidebar colors, fonts, grid layout, etc.) expect to replicate the edit across all HTML
files individually rather than editing one shared source.
### Current Vidensbase order
`CSharp.html` (with `fagord.html` and `Grundbegreber.html` as sub-links) → `UML.html` → `UnifiedProcess.html` →
`HTML-Guides.html` → `CSS-Styling.html` → `Ubuntu.html` (with `Rider.html`, `ShellLearning.html`,
`EnvironmentConfiguration.html`, and `HurtigeGenveje.html` as sub-links) → `Python.html` →
`Windows.html` (with `VisualStudio.html` and `WSL.html` as sub-links). IDE sub-links are grouped by
the OS they're mainly used on (Rider under Ubuntu since it's cross-platform and commonly run on
Linux; Visual Studio under Windows since it's Windows-specific) rather than under C# Learning.
### UML.html and UnifiedProcess.html
Notes for a school subject on UML and Unified Process (UP), which the user follows closely in their
coursework. `UML.html` covers class diagrams (visibility symbols, association/aggregation/composition/
generalization/dependency relationships, multiplicity), use case diagrams (actor, use case, include/
extend), sequence diagrams, and activity diagrams. `UnifiedProcess.html` covers UP's four phases
(Inception, Elaboration, Construction, Transition), its iterative/incremental nature, and its nine
disciplines (Business Modeling, Requirements, Analysis & Design, Implementation, Test, Deployment,
Configuration & Change Management, Project Management, Environment). The two pages cross-link each
other via their "Hurtige genveje" cards, since UP's use-case-driven approach ties directly back to
UML's use case diagrams.
### Fagord.html and Grundbegreber.html
Both are C# Learning sub-pages, and both draw on the same set of basics (variables, conditions,
loops, methods, classes/objects, constructors, arrays, etc.) — they're intentionally not the same
page, so don't try to merge them. `Fagord.html` is a Danish/English terminology glossary for oral
exam prep (see below). `Grundbegreber.html` is a personal progress checklist (✅-prefixed `.checklist`
items) of what the user has actually studied/worked on over a specific stretch of time — recreated
after they lost the physical sticky note it was originally written on. When the user reports learning
something new, check whether it belongs as a new ✅ entry on Grundbegreber.html.

Fagord.html: Danish/English glossary of C# terminology (Klasse/Class, Objekt/Object, Konstruktør/
Constructor, Array, Metode/Method, Variabel/Variable, Indkapsling/Encapsulation, Arv/Inheritance,
Løkke/Loop, Betingelse/Conditional). Exists because the user was marked down in a prior exam for not
using proper terminology when defending their code orally, despite being able to read/understand code
well. Each entry explains the underlying concept (not just what the line of code does — what the
programmer has actually done), not just syntax, and pairs Danish and English terms so the user can
practice
saying them aloud. New entries should follow this same pattern and keep the `.reference` box blank
for the user to fill in from their own textbook (currently: *C# 10.0 All-in-One For Dummies*).
### Ubuntu.html and its sub-pages
`Ubuntu.html` itself only holds the "10 grundlæggende Linux-kommandoer" (basic commands) list now —
"Shell Learning" (pipes/redirection, globbing, env vars, job control, shebang, aliases, history) and
"Environment Configuration" (`.bashrc` vs `.profile`, `$PATH`, `export`, `PS1`, `source`, dotfiles)
were split out into their own sub-pages, `ShellLearning.html` and `EnvironmentConfiguration.html`,
sidebar-linked as `sub-link`s under Ubuntu alongside `Rider.html`. A fourth sub-link,
`HurtigeGenveje.html`, holds basic terminal keyboard shortcuts (Ctrl+C, Ctrl+R reverse search, Tab
completion, `!!`, `cd -`, etc.) — note this is a distinct dedicated page from the "Hurtige genveje"
`.grid-links` shortcut-card widget every page has at the bottom; don't conflate the two when editing.
All four of these pages use the same blank `.reference` citation pattern as Fagord.html, sourced from
*The Linux Command Line* (William Shotts) — never copy text from this book verbatim onto a page
(copyright); write original summaries/notes instead, and leave the chapter/page in the `.reference`
box for the user to fill in by hand.
### Opdateringer.html
Blog-style changelog (renamed from "Daglige Notater" since updates don't happen daily). Newest post
goes at the top, directly under the callout tip box; older posts stay below it. Keep entries short
and factual — no references to what was learned at a job/employer (the user has asked this be kept
generic/neutral, since the site is public).
### Images
Screenshots and other images go in `billeder/` (see `billeder/README.md` for naming convention and
the `.screenshot` CSS snippet to reuse). Not yet used on any page as of this writing.
