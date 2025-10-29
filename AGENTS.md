# Repository Guidelines

## Project Structure & Module Organization
Keep exploratory work in the tracked notebooks `lesson2.ipynb` and `test.ipynb`. When code becomes reusable, refactor it into modules under a `src/` package (create it if absent) so notebooks stay light and import shared helpers. Store datasets or generated artifacts in a dedicated `data/` directory with `.gitignore` entries for large or transient files. Mirror the Python package layout in `tests/` so every module has a corresponding `test_*.py` file that exercises its public API.

## Build, Test, and Development Commands
Use an isolated environment before installing dependencies: `python -m venv .venv && source .venv/bin/activate`. Track runtime libraries in `requirements.txt` and install them with `pip install -r requirements.txt`. Run the notebook server during exploratory work with `jupyter lab` (or `jupyter notebook`). Execute the automated suite with `pytest` from the repository root; add `-q` for concise output or `--maxfail=1` while iterating. For coverage snapshots, run `pytest --cov=src --cov-report=term-missing`.

## Coding Style & Naming Conventions
Follow PEP 8 with 4-space indentation and descriptive, snake_case names for functions and variables. Use CapWords for classes and keep module names lowercase. Format Python files with `black` and order imports with `isort`; if you touch notebooks, strip noisy output before committing. Prefer pure functions that can be tested independently of notebook state, and document non-obvious behaviors with docstrings or short comments.

## Testing Guidelines
Author tests with `pytest`, placing them under `tests/` and naming files `test_<feature>.py`. Individual tests should read `test_<behavior>` and assert observable outcomes rather than internal state. When adding new helpers in `src/`, provide at least one unit test plus an integration-style check when interactions span multiple modules. Aim for 80% statement coverage and justify any exclusions via `# pragma: no cover`.

## Commit & Pull Request Guidelines
Write commit subjects in the imperative mood (e.g., "Add normalization helper") and keep them under 72 characters. Bundle related notebook and module updates together so reviewers can replicate results. Pull requests should summarize the change, reference related issues, note any data dependencies, and include screenshots or terminal snippets for notable notebook output. Confirm that `pytest` succeeds before requesting review.

## Notebook Hygiene
Clear expensive outputs, pin random seeds where reproducibility matters, and move secrets or credentials into environment variables referenced via `os.environ`. Prefer lightweight CSV samples checked into `data/` for examples, leaving large datasets in external storage with documented retrieval steps.
