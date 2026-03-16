# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic CV generator that produces both PDF (via LaTeX) and Markdown/HTML from a single YAML data source (`cv.yaml`) and BibTeX bibliography (`publications/all.bib`).

## Build Commands

```bash
make all        # Generate both PDF and Markdown outputs
make public     # Generate public version only
make stage      # Stage files to website repository
make push       # Push updated documents to website
make clean      # Remove build artifacts
make viewpdf    # Open generated PDF
```

Build output goes to `build/` (cv.pdf, cv.tex, cv.md).

## Architecture

**Data flow:** `cv.yaml` + `publications/all.bib` → `generate.py` (Jinja2) → `.tex`/`.md` → `latexmk`/`biber` → PDF

- **`cv.yaml`** — single source of truth for all CV content
- **`generate.py`** — main build script; uses `RenderContext` class to manage Jinja2 environments for LaTeX and Markdown contexts
- **`templates/latex/`** — LaTeX templates using custom Jinja delimiters (`~<...>~` for blocks, `<<...>>` for variables) to avoid LaTeX conflicts
- **`templates/markdown/`** — Markdown templates using standard Jinja delimiters
- **`publications/all.bib`** — BibTeX database; parsed by `bibtexparser`

## Key Details

- LaTeX output uses the `moderncv` document class
- `generate.py` includes text replacement rules for converting LaTeX formatting to Markdown (e.g., `\href{}{}` → HTML links)
- GitHub repo star counts and Google Scholar citation stats are scraped and cached via Python `shelve` database
- Dependencies: `pip install -r requirements.txt` (bibtexparser, Jinja2, PyYAML, beautifulsoup4, scholarly)
- External tools needed: `latexmk`, `biber`, `python3`
