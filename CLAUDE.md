# Colab Recipes — conventions

This repo is a small library of Google Colab notebooks, one job each. Keep it simple; do not add frameworks, packages or CI.

The repo is **public** (`margani/colab-recipes`). Anything committed, including history, is visible to everyone.

## Structure
- `notebooks/<category>/<kebab-case-name>.ipynb` — one recipe per file. Categories are short nouns: `drive`, `files`, `media`, `pdf`, `web`, `data`. A new category needs a new folder and a new README section.
- `templates/recipe-template.ipynb` — start every new recipe from this.
- `README.md` — the index, one `## <category>` section per category folder, in the same order. Every recipe must have a row in its category's table with an "Open in Colab" badge (`https://colab.research.google.com/github/margani/colab-recipes/blob/main/<path>`). The description column is one short line.

## One job per notebook
- A notebook does exactly one job. A follow-up task (verify a checksum, extract an archive, convert a file) is its own recipe, not an extra step in another notebook.
- Only the steps the job needs. Drop a step that another step already covers (e.g. no Rename step when Download already takes a file name).
- Don't add "nice to have" steps. Ask the owner first.

## Notebook rules
- Everything is in English: `#@title` labels, printed messages, code and comments.
- Minimal text. The notebook is:
  1. One markdown cell with only the recipe name: `# Download URL to Google Drive`.
  2. One code cell per step. The step's `#@title` is its only label, a short verb phrase: `Connect Google Drive`, `Check free space`, `Download`, `Verify`, `Extract`.
- No explanatory markdown, no instructions, no section numbers, no "(optional)" labels, no emoji headings. The steps are obvious; the form fields explain themselves.
- Printed messages are short: `Saving to: …`, `✅ Match`, `Enter a URL.`
- The first step is always `Connect Google Drive` if the recipe touches Drive.
- Path fields accept a path relative to My Drive, as Drive shows it (`Temp/video.mp4`, `Temp\video.mp4`, `My Drive/Temp/video.mp4`, with or without quotes), or a full `/content/...` path. Every input-path cell normalizes this right after its form fields. Destination folders for downloads are relative to `MyDrive`. Outputs go next to the input (`video-small.mp4`, `scan-ocr.pdf`).
- An empty required field stops with a short message (`Enter a file path.`), not a traceback.
- Every user-supplied value is a Colab form field (`#@param`) at the top of its cell, and every code cell has `#@title` and `"cellView": "form"` metadata.
- Cells must be safe to re-run (use `wget -c`, `mkdir -p`, `exist_ok=True`, and guard steps that move or rename files).
- Strip outputs before committing (`"outputs": []`, `"execution_count": null`); outputs can leak Drive paths and file names into the public repo.
- `metadata.colab.name` equals the file name.
- No secrets in notebooks. If a token is needed, read it with `google.colab.userdata.get(...)` (Colab Secrets).

## When adding or changing a recipe
1. Open an issue, then a branch, then a PR that says `Closes #n`. Squash-merge it yourself once checks pass, then delete the branch.
2. Copy the template, keep the step pattern.
3. Validate JSON: `python -c "import json,sys;json.load(open(sys.argv[1]))" <file>`.
4. Check the rules above on every notebook: one top markdown cell, then code cells only, each with `#@title` and form view, empty outputs, no non-English text.
5. Run changed cell code locally where it doesn't need Colab (hashing, renaming, path logic) with test files, twice, to prove it is re-run safe.
6. Update the README row in its category section, and check every badge path exists on `main` after merge.
7. Update the dashboard status file (`~/projects/personal/projects-dashboard/status/colab-recipes.json`) as `STATUS_INSTRUCTIONS.md` describes.

## Lessons
- 2026-10-26: The first version had Persian, chatty markdown with numbered sections and bundled download, verify, extract and rename in one notebook. The owner wanted English, bare step titles and one job per notebook. The rules above come from that review.
- 2026-10-26: compress-video failed with `Not a file: Temp\video_….mp4` because input paths had to be full `/content/drive/MyDrive/...` paths. Users type paths relative to My Drive, often with Windows backslashes; test path fields with that form, not only full paths.
