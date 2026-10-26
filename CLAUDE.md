# Colab Recipes — conventions

This repo is a small library of Google Colab notebooks, one job each. Keep it simple; do not add frameworks, packages or CI.

## Structure
- `notebooks/<category>/<kebab-case-name>.ipynb` — one recipe per file. Categories are short nouns: `drive`, `media`, `files`, `data`, `web`.
- `templates/recipe-template.ipynb` — start every new recipe from this.
- `README.md` — the index. Every recipe must have a row with an "Open in Colab" badge (`https://colab.research.google.com/github/<user>/colab-recipes/blob/main/<path>`).

## Notebook rules
- Markdown cells are in Persian. Every Persian line must start with a Persian letter (not an emoji, number or Latin word) so RTL renders correctly; put emoji at the end of the line.
- Code, variable names and comments are in English.
- Section 1 is always "mount Google Drive" if the recipe touches Drive.
- Every user-supplied value is a Colab form field (`#@param`) at the top of its cell, and every code cell has `#@title` and `"cellView": "form"` metadata.
- Sections are numbered (`## ۱.`, `## ۲.`), optional ones say so.
- Cells must be safe to re-run (use `wget -c`, `mkdir -p`, `exist_ok=True`).
- Strip outputs before committing (`"outputs": []`, `"execution_count": null`).
- No secrets in notebooks. If a token is needed, read it with `google.colab.userdata.get(...)` (Colab Secrets).

## When adding or changing a recipe
1. Copy the template, keep the section pattern.
2. Validate JSON: `python -c "import json,sys;json.load(open(sys.argv[1]))" <file>`.
3. Update the README index row.
