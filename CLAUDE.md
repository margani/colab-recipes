# Colab Recipes — conventions

This repo is a small library of Google Colab notebooks, one job each. Keep it simple; do not add frameworks, packages or CI.

## Structure
- `notebooks/<category>/<kebab-case-name>.ipynb` — one recipe per file. Categories are short nouns: `drive`, `media`, `files`, `data`, `web`.
- `templates/recipe-template.ipynb` — start every new recipe from this.
- `README.md` — the index. Every recipe must have a row with an "Open in Colab" badge (`https://colab.research.google.com/github/<user>/colab-recipes/blob/main/<path>`).

## Notebook rules
- Everything is in English: `#@title` labels, printed messages, code and comments.
- Minimal text: one markdown cell at the top with the recipe name (`# Download URL to Google Drive`), then one code cell per step. The step's `#@title` is its only label (`Connect Google Drive`, `Check free space`, `Download`). No explanatory markdown.
- The first step is always "Connect Google Drive" if the recipe touches Drive.
- Every user-supplied value is a Colab form field (`#@param`) at the top of its cell, and every code cell has `#@title` and `"cellView": "form"` metadata.
- Cells must be safe to re-run (use `wget -c`, `mkdir -p`, `exist_ok=True`).
- Strip outputs before committing (`"outputs": []`, `"execution_count": null`).
- No secrets in notebooks. If a token is needed, read it with `google.colab.userdata.get(...)` (Colab Secrets).

## When adding or changing a recipe
1. Copy the template, keep the step pattern.
2. Validate JSON: `python -c "import json,sys;json.load(open(sys.argv[1]))" <file>`.
3. Update the README index row.
