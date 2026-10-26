# Colab Recipes

Reusable Google Colab notebooks. One notebook = one job.
Open any notebook straight from GitHub in Colab; nothing to install.

## Index

| Category | Recipe | What it does | Open |
|---|---|---|---|
| drive | [download-url-to-drive](notebooks/drive/download-url-to-drive.ipynb) | Download a file from a direct URL into Google Drive | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/margani/colab-recipes/blob/main/notebooks/drive/download-url-to-drive.ipynb) |
| files | [extract-archive](notebooks/files/extract-archive.ipynb) | Extract a zip, 7z or rar archive in Google Drive | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/margani/colab-recipes/blob/main/notebooks/files/extract-archive.ipynb) |
| files | [verify-sha256](notebooks/files/verify-sha256.ipynb) | Check a Drive file's SHA256 against an expected value | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/margani/colab-recipes/blob/main/notebooks/files/verify-sha256.ipynb) |

## Adding a recipe

1. Copy `templates/recipe-template.ipynb` into `notebooks/<category>/<kebab-name>.ipynb`.
2. Fill it in (forms via `#@param`, no hard-coded values).
3. Add a row to the index above.
