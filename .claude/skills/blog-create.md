# Create Blog Post

Create a new Quarto blog post as a Jupyter notebook.

## Usage

`/blog-create <topic>` — Creates a new blog post about the given topic.

## Instructions

When this skill is invoked:

1. **Determine the post slug** from the topic. Use lowercase, hyphenated format (e.g., "pytorch-autograd", "transformer-attention").

2. **Create the post directory**: `posts/<slug>/`

3. **Create `posts/<slug>/index.ipynb`** as a Jupyter notebook with:
   - A **raw cell** as the first cell containing YAML front matter:
     ```
     ---
     title: "<Post Title>"
     author: "Anindya Saha"
     date: "<today's date in YYYY-MM-DD>"
     categories: [<relevant-categories>]
     description: "<one-line description>"
     ---
     ```
   - **Markdown cells** for explanations and section headers
   - **Code cells** with runnable Python code demonstrating the concepts
   - Keep the post **minimal and focused** — aim for 5-7 sections max
   - All code cells should be executable and self-contained

4. **Install any new dependencies** if needed:
   - Add them to `pyproject.toml` under `[project] dependencies`
   - Run `uv sync` to install

5. **Execute the notebook** to bake in outputs:
   ```
   source .venv/bin/activate
   export PATH="/home/asaha/quarto-1.6.42/bin:$PATH"
   quarto render posts/<slug>/index.ipynb --execute
   ```

6. Confirm the post was created and ask if the user wants to publish it (invoke `/blog-publish`).

## Notes

- The virtual environment is at `.venv/` — always activate it before rendering
- Quarto is at `/home/asaha/quarto-1.6.42/bin/quarto`
- Use `uv` for dependency management, not pip
