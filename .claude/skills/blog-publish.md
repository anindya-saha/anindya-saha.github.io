# Publish Blog

Render the Quarto site and publish to GitHub Pages.

## Usage

`/blog-publish` — Renders the full site and pushes to GitHub.

## Instructions

When this skill is invoked:

1. **Activate the environment and render the full site**:
   ```bash
   source .venv/bin/activate
   export PATH="/home/asaha/quarto-1.6.42/bin:$PATH"
   quarto render
   ```
   This renders all posts and outputs to `docs/`. The `_quarto.yml` post-render hook automatically creates `docs/.nojekyll`.

2. **Verify the render succeeded** — check that `docs/index.html` exists and the new post's HTML is in `docs/posts/<slug>/`.

3. **Commit all changes** (source notebooks + rendered output in `docs/`):
   ```bash
   git add posts/ docs/ _quarto.yml pyproject.toml uv.lock
   git commit -m "<descriptive commit message>"
   ```

4. **Push to GitHub**:
   ```bash
   git push origin main
   ```

5. **Report the URL** — the post will be live at `https://anindya-saha.github.io/posts/<slug>/` after GitHub Pages rebuilds (1-2 minutes).

## Notes

- GitHub Pages serves from `docs/` on the `main` branch
- The `.nojekyll` file is critical — without it, `site_libs/` won't load (CSS/JS breaks)
- Always render the full site (`quarto render`), not just a single post, so the listing page and search index update
