# CLAUDE.md

## Project Overview

Personal blog at https://anindya-saha.github.io/, built with **Quarto** and **Jupyter notebooks**, deployed via GitHub Pages.

## Tech Stack

- **Quarto** (v1.6.42) — static site generator, installed at `/home/asaha/quarto-1.6.42/bin/quarto`
- **Jupyter notebooks** (`.ipynb`) — blog post format
- **uv** — Python dependency management (`pyproject.toml` + `uv.lock`)
- **GitHub Pages** — serves from `docs/` on `main` branch

## Project Structure

```
_quarto.yml          # Site config (theme, navbar, post-render hooks)
index.qmd            # Blog listing page (auto-lists posts/)
about.qmd            # About page
styles.css           # Custom CSS
pyproject.toml       # Python deps (torch, matplotlib, jupyter, etc.)
posts/               # Blog posts — each post is posts/<slug>/index.ipynb
docs/                # Rendered output (committed, served by GitHub Pages)
.claude/skills/      # Claude Code skills for blog workflow
```

## Common Commands

```bash
# Activate environment
source .venv/bin/activate
export PATH="/home/asaha/quarto-1.6.42/bin:$PATH"

# Install/sync dependencies
uv sync --extra notebook

# Preview locally
quarto preview

# Render full site
quarto render

# Render single post
quarto render posts/<slug>/index.ipynb --execute
```

## Blog Workflow

1. Create a new post: `posts/<slug>/index.ipynb` with YAML front matter in a raw cell
2. Render: `quarto render`
3. Commit and push: rendered output goes to `docs/`

Use `/blog-create <topic>` and `/blog-publish` skills for the full workflow.

## Important Notes

- `docs/.nojekyll` must exist — the `_quarto.yml` post-render hook handles this
- Always render the full site so the listing page and search index update
- PyTorch index is configured for CUDA 12.8 in `pyproject.toml` (`[tool.uv.sources]`)
