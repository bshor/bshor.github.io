# CLAUDE.md — Dr. Boris Shor's Academic Website

## Project Overview

Quarto-based academic website for Dr. Boris Shor (political scientist). Generates a static HTML site in `docs/` for hosting on GitHub Pages at https://bshor.github.io.

## Tech Stack

- **Framework:** Quarto (`.qmd` files, YAML config)
- **Theme:** Cosmo
- **Languages:** Markdown/QMD, YAML, CSS, JavaScript
- **Bibliography:** BibTeX (`references.bib`, `working.bib`) with `apsr-reverse.csl`
- **Extensions:** `mcanouil/iconify`, `quarto-ext/fontawesome`, `schochastics/academicons`
- **Deployment:** GitHub Pages from `docs/` directory

## Key Files & Directories

| Path | Purpose |
|------|---------|
| `_quarto.yml` | Main config: nav, theme, output dir, bibliography |
| `index.qmd` | Landing/about page |
| `publications.qmd` | Publications page (auto-lists all `references.bib` entries) |
| `working.qmd` | Working papers page (from `working.bib`) |
| `teaching.qmd` | Teaching/courses page |
| `projects.qmd` | Grants page (data from `projects.yml`) |
| `data.qmd` | Datasets page (links to Harvard Dataverse) |
| `people.qmd` | Team members page |
| `contact.qmd` | Contact info |
| `references.bib` | Main publications bibliography (~286 entries) |
| `working.bib` | Working papers bibliography |
| `projects.yml` | Grants/projects data |
| `people/` | YAML files per role: `pi.yml`, `phd-student.yml`, `phd-alumni.yml`, etc. |
| `posts/` | Blog posts/news (one subdirectory per post with `index.qmd`) |
| `files/` | Static assets: CV PDF, papers PDFs, images, profile photos |
| `files/includes/_academic.qmd` | Loads Academicons, Font Awesome, Altmetric/Dimensions badges |
| `styles.css` | Primary custom CSS (abstract styling, etc.) |
| `custom.css` | Additional custom styles |
| `docs/` | **Generated output — do not edit manually** |

## Development Workflow

```bash
quarto preview    # Local dev server with auto-reload
quarto render     # Build full site to docs/
```

After rendering, commit and push `docs/` to deploy via GitHub Pages.

## Content Management Patterns

### Publications
- Add entries to `references.bib` (BibTeX format)
- `publications.qmd` uses `nocite: '@*'` — all entries appear automatically
- Abstracts use `[ABSTRACT-START]...[ABSTRACT-END]` markers; JavaScript collapses them

### Working Papers
- Add entries to `working.bib`
- Same abstract toggle pattern as publications

### People
- Edit YAML files in `people/` directory (one file per role category)
- `people.qmd` uses Quarto listings to render from these files
- Profile photos go in `files/profiles/`

### Posts/News
- Create `posts/<post-slug>/index.qmd`
- `posts/_metadata.yml` sets `freeze: true` and `draft-mode: unlinked` for all posts

### Papers/PDFs
- Place PDFs in `files/papers/`
- This directory is declared as a resource in `_quarto.yml` so it's copied to output

## Important Implementation Details

- **Abstract toggles:** JavaScript in `publications.qmd`/`working.qmd` wraps `[ABSTRACT-START]...[ABSTRACT-END]` blocks in collapsible `<details>` elements
- **Dynamic year in footer:** Inline `<script>` writes current year
- **Altmetric/Dimensions badges:** Loaded via `files/includes/_academic.qmd` in `<head>`
- **Draft mode:** `draft-mode: unlinked` hides drafts from navigation without breaking builds
- **Email obfuscation:** Configured as `javascript` in `_quarto.yml`
- **External links:** Open in new window; `link-external-filter` exempts `bshor.github.io/custom`

## Navigation Structure

- **Left navbar:** Publications → Data → Working Papers → Grants → Teaching
- **Right navbar:** CV (PDF link), GitHub icon, Twitter/X link
- **Footer:** Copyright (Dr. Shor) + GitHub icon

## Deployment

1. `quarto render`
2. `git add docs/ && git commit -m "..."`
3. `git push`
4. GitHub Pages serves from `/docs` folder on `main` branch
