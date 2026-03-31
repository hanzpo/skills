---
name: python
description: Provides guidelines for writing code in Python. Use when writing Python.
---

When writing Python, use type hints on all function signatures (parameters and return types) and class attributes. Avoid annotating local variables where the type is obvious from context.

## Project Setup

- Always use **uv** for project and dependency management.
- For new projects, initialize with `uv init` — this scaffolds `pyproject.toml`, `.python-version`, and a virtual environment automatically.
- Use `uv add <package>` to add dependencies and `uv sync` to install from the lockfile. Do NOT use `uv pip install` or raw `pip install` — the `uv pip` interface is a compatibility escape hatch, not the default workflow.
- Use `uv run <command>` to execute scripts/tools within the project's virtual environment (e.g., `uv run pytest`, `uv run python main.py`).
- Pin the Python version in `.python-version`. uv will automatically download and manage it.
- All project metadata, dependencies, and tool configuration belong in `pyproject.toml`. Do not create `setup.py`, `setup.cfg`, or `requirements.txt`.

## Project Structure

- Use the `src` layout: place your package under `src/<package_name>/` to avoid accidental local imports shadowing the installed package.
- Define `__all__` in `__init__.py` files to explicitly declare the public API of each module.

## Linting & Formatting

- Use **Ruff** for both linting (`ruff check`) and formatting (`ruff format`). Do not use flake8, isort, black, or autopep8.
- Configure Ruff in `pyproject.toml` under `[tool.ruff]`.

## Type Checking

- Use **pyright** for static type analysis. Configure it in `pyproject.toml` under `[tool.pyright]` or in `pyrightconfig.json`.
- Prefer `"typeCheckingMode": "strict"` for new projects.
- Use `typing.Self`, `typing.TypeAlias`, `X | Y` union syntax (3.10+), and `type` statement (3.12+) where appropriate.

## Code Style

- Use `@dataclass` for plain structured data. Use **Pydantic** `BaseModel` when you need validation, serialization, or parsing (APIs, configs, external data).
- Do not pass raw `dict`s around as structured data — define a proper type.
- Use `pathlib.Path` instead of `os.path` for all filesystem operations.
- Use f-strings for string formatting. Do not use `.format()` or `%`-style formatting.
- Use `match`/`case` (3.10+) for branching on structured data, tagged unions, or command dispatch instead of if/elif chains.
- Prefer `asyncio` with `async`/`await` for I/O-bound concurrency. Use `httpx` over `requests` when async support is needed.
- Use context managers (`with` statements) for resource management (files, connections, locks).
- Use list/dict/set comprehensions over `map()`/`filter()` with lambdas.
- Raise specific exception types. Avoid bare `except:` and `except Exception:` unless re-raising.

## Testing

- Use **pytest** as the test framework. Do not use `unittest` unless extending an existing `unittest`-based suite.
- Run tests with `uv run pytest`.
- Place tests in a top-level `tests/` directory mirroring the `src/` package structure.
