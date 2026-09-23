# Repository Guidelines

## Project Structure & Module Organization

Prophetverse is a Poetry-managed Python package using a `src/` layout. Core code lives in `src/prophetverse/`, organized by engines, effects, forecasting interfaces, datasets, utilities, and experimental features. Tests mirror these areas under `tests/` (for example, `tests/effects/` and `tests/engine/`). Documentation source is in `docs/` and is rendered with Quarto; reusable extension templates are in `extension_templates/`. Keep new public functionality in the appropriate package submodule and add or update its focused tests and documentation.

## Build, Test, and Development Commands

Install the package and development tools with:

```bash
poetry install --extras dev
```

Run the full test suite with coverage, matching CI:

```bash
PYTHONPATH=src poetry run pytest --cov=prophetverse --cov-report=xml -m "not smoke" --durations=10
```

Run a faster local subset with `PYTHONPATH=src poetry run pytest -m smoke`, or target a module such as `PYTHONPATH=src poetry run pytest tests/effects/test_adstock.py`. Build documentation with `quarto render docs`. Run changed-file checks with `pre-commit run --files <path>`, and run slower manual checks with `pre-commit run --hook-stage manual --all-files`.

## Coding Style & Naming Conventions

Use Python 3.9-compatible syntax, four-space indentation, type hints, and NumPy-style docstrings. Black formats code to 88 columns; isort uses the Black profile. Use `snake_case` for functions, variables, and modules; `PascalCase` for classes; and descriptive test names beginning with `test_`. Keep imports sorted and run the configured pre-commit hooks before opening a PR.

## Testing Guidelines

Tests use pytest and are organized by feature. Add regression coverage for bug fixes and unit tests for new effects, engines, or utilities. Mark intentionally fast tests with `@pytest.mark.smoke`; use `@pytest.mark.ci` for CI-specific cases. CI collects coverage for `prophetverse`, so maintain meaningful coverage for changed paths.

## Commit & Pull Request Guidelines

Commits generally use a bracketed conventional prefix, such as `[ENH] Add ...`, `[MNT] ...`, or `[DOC] ...`; keep messages concise and imperative. Pull requests should reference an issue for non-trivial work, explain the change and validation performed, include appropriate tests, and remain focused. Ensure CI and formatting checks are green before requesting review. Documentation or UI changes should include rendered output or screenshots when useful.

## Security & Configuration Tips

Do not commit credentials, private keys, generated coverage files, or large data artifacts. Keep dependency and Python-version changes synchronized with `pyproject.toml` and CI workflows, and preserve the package’s `src` import configuration when running tools locally.
