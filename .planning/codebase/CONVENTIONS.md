# Coding Conventions

**Analysis Date:** 2026-04-20

## Naming Patterns

**Files:**

- Module files are `snake_case.py` grouped by domain noun, e.g. `mesmo/electric_grid_models.py`, `mesmo/thermal_grid_models.py`, `mesmo/der_models.py`, `mesmo/data_interface.py`, `mesmo/problems.py`, `mesmo/solutions.py`, `mesmo/plots.py`, `mesmo/utils.py`, `mesmo/api.py`, `mesmo/config.py`.
- One flat layer under `mesmo/` — no subpackages. Each module file is typically large (500–4500 lines) and groups related classes/functions together.
- Test files mirror module names with a `test_` prefix, e.g. `tests/test_der_models.py`, `tests/test_electric_grid_models.py`, `tests/test_data_interface.py`.
- Example scripts use `run_<action>_<scope>.py`, e.g. `examples/run_api_nominal_operation_problem.py`, `examples/run_electric_grid_optimal_operation.py`. Validation scripts use `validation_<scope>.py`, e.g. `examples/validation_linear_electric_grid_model.py`.
- SQL schema lives alongside source: `mesmo/data_schema.sql`. Default YAML config: `mesmo/config_default.yml`.

**Functions:**

- `snake_case` verb-first, e.g. `run_nominal_operation_problem`, `recreate_database`, `connect_database`, `get_logger`, `get_results_path`, `get_index`, `write_figure_plotly`, `chunk_list`, `ray_starmap`, `log_time`.
- Constructor-like factory functions that return an instance of another module's class use the class name as a proxy (e.g. `mesmo.utils.OptimizationProblem()` in `mesmo/utils.py:570` is a deprecated shim that returns `mesmo.solutions.OptimizationProblem`).
- Private/internal helpers are not prefixed with `_` — the codebase relies on module structure rather than name mangling.

**Variables:**

- `snake_case` throughout. Domain terms are spelled out (no abbreviations), e.g. `der_data`, `scenario_name`, `electric_grid_model`, `active_power_nominal_timeseries`, `branch_power_vector_1`, `linear_electric_grid_model_method`.
- Loop indexes use short names (`i`, `j`) only inside comprehensions; otherwise use descriptive names (`attribute_name`, `csv_file`, `data_path`).
- Boolean flags are prefixed with `is_`, e.g. `is_electric_grid_connected`, `is_thermal_grid_connected`, `is_standalone`.

**Types / Classes:**

- `CapWords` (PascalCase), e.g. `ObjectBase`, `ResultsBase`, `ProblemBase`, `DERModel`, `DERModelSet`, `ElectricGridModel`, `NominalOperationProblem`, `OptimalOperationProblem`, `OptimizationProblem`, `ScenarioData`, `PriceData`.
- Abstract-base classes end in `Base`, e.g. `ObjectBase`, `ResultsBase`, `ProblemBase` (pattern used by `tests/test_problems.py` to exclude them via `not object_name.endswith("Base")`).
- Results container classes end in `Results` (e.g. `ElectricGridOperationResults`, `ElectricGridDLMPResults`).
- Dict-of-objects containers end in `Dict` (e.g. `ResultsDict`, `ProblemDict`).
- Acronyms keep caps: `DER`, `API`, `DLMP` (e.g. `DERModelSet`, `FixedEVChargerModel`).

## Code Style

**Formatting:**

- **No black / ruff / isort / flake8 config exists.** Only `pylint` is declared in `pyproject.toml`.
- **Max line length: 120** — set via `[tool.pylint.FORMAT]` `max-line-length = 120` in `pyproject.toml:62-63`.
- 4-space indentation, double quotes for strings, trailing commas in multi-line lists/dicts/call args.
- Blank line after each section of in-function comments (see `mesmo/api.py:20-46` for canonical "comment-per-block" style).

**Linting:**

- **Tool:** `pylint` (declared in `[project.optional-dependencies]` under `"tests"` in `pyproject.toml:46`).
- **Disabled rules** (`pyproject.toml:65-74`):
  - `function-redefined` — allows `multimethod` overloads.
  - `logging-fstring-interpolation` — f-strings in `logger.info(...)` are permitted.
  - `no-value-for-parameter` — `multimethod` dispatch confuses pylint.
  - `non-parent-init-called`, `super-init-not-called` — grid model classes skip `super().__init__` intentionally.
  - `too-many-function-args`, `too-many-lines` — large modules are acceptable.
- Pylint is installed but **not run in CI** (CI only runs `coverage run -m unittest discover tests`; see `.github/workflows/pythontests.yml:32-36`). Run locally via `pylint mesmo/`.

## Import Organization

**Order** (observed pattern — stdlib, then third-party, then first-party; `mesmo` imports are a separate trailing block; no isort config enforces this):

1. Standard library imports (`import copy`, `import itertools`, `import pathlib`, `import typing`, `import sqlite3`).
2. Third-party imports, grouped with stdlib — **alphabetical by module name**, mixed `import` / `from` styles (e.g. `mesmo/electric_grid_models.py:3-11`: `itertools`, `multimethod`, `natsort`, `numpy as np`, `opendssdirect`, `pandas as pd`, `scipy.sparse as sp`, `scipy.sparse.linalg`, `typing`).
3. **Blank line**, then first-party `mesmo.*` imports (e.g. `import mesmo.config`, `import mesmo.data_interface`, `import mesmo.utils`). See `mesmo/problems.py:10-16`, `mesmo/der_models.py:13-18`.

**Style:**

- Prefer `import mesmo.config` over `from mesmo import config`. All references use the full dotted path (`mesmo.config.config[...]`, `mesmo.utils.log_time(...)`). This is a firm project convention.
- Standard aliases only: `numpy as np`, `pandas as pd`, `scipy.sparse as sp`, `plotly.graph_objects as go`, `plotly.io as pio`, `cvxpy as cp`, `gurobipy as gp`.
- `from multimethod import multimethod` is the one common `from` import for third-party code (used in `mesmo/problems.py`, `mesmo/der_models.py`, `mesmo/data_interface.py`, `mesmo/electric_grid_models.py`).
- Avoid circular-import issues by lazy-importing inside functions. Example: `mesmo/utils.py:576` imports `mesmo.solutions` inside the `OptimizationProblem()` shim function.

**Path aliases:**

- None. Python imports only. The in-code "path" concept refers to the `base_path / "mesmo" / ...` construction in `mesmo/config.py:100` and `config["paths"]["data"]`, not to import aliases.

## Error Handling

**Pattern:** Raise built-in exceptions with f-string messages that name the offending value. No custom exception hierarchy.

**Exception types observed in `mesmo/`:**

- `ValueError` — most common; used for invalid enum-like string args, empty lookups, unknown configuration. See `mesmo/utils.py:302`, `mesmo/config.py:82`, `mesmo/problems.py:367,486`, `mesmo/data_interface.py:180,430,596,638,901,912`, `mesmo/electric_grid_models.py:333,445,491,580,588,1088,3057`.
- `TypeError` — invalid argument type, e.g. `mesmo/utils.py:335` `raise TypeError(f"Invalid index set type: {type(index_set)}")`.
- `NotImplementedError` — unimplemented abstract methods and unsupported model branches. See `mesmo/problems.py:41,44`, `mesmo/electric_grid_models.py:1662,4508`.
- `AssertionError` — invariant violations on DER model construction, e.g. `mesmo/der_models.py:201,219,237`.
- `NameError`, `ImportError`, `FileNotFoundError` — resource/file errors. See `mesmo/data_interface.py:110,117`, `mesmo/utils.py:527`.

**Message format:**

- f-string, typically naming the bad value: `raise ValueError(f"Unknown transformer type: {transformer.at['connection']}")`.
- Chained exceptions use `from exception` to preserve cause: `raise ImportError(f"Error loading {csv_file} into database.") from exception` (`mesmo/data_interface.py:117`).

`**try` / `except`:**

- Rarely used — only for genuine fallbacks (old-pandas compatibility in `mesmo/config.py:134-138`, optional `TypeError` catch in `mesmo/utils.py:256`).
- **Do not swallow exceptions silently.** If catching, either re-raise with `from` or explain via a comment.
- **Do not use `except Exception:`** — target the specific error class.

**Validation style:**

- Validate at the top of the function and `raise` early with a descriptive message. Example `mesmo/utils.py:371-373`:

```python
if raise_empty_index_error:
    if not (len(index) > 0):
        raise ValueError(f"Empty index returned for: {levels_values}")
```

## Logging

**Framework:** Python stdlib `logging`, obtained via the project factory `mesmo.config.get_logger(__name__)` (`mesmo/config.py:64-84`).

**Module-level setup:** Every module that logs starts with:

```python
logger = mesmo.config.get_logger(__name__)
```

See `mesmo/api.py:8`, `mesmo/utils.py:26`, `mesmo/problems.py:18`, `mesmo/der_models.py:20`, all test modules.

**Log level resolution:** Driven by `config["logs"]["level"]` from `mesmo/config_default.yml` (values `debug`, `info`, `warn`, `error`). Unknown values raise `ValueError` in `get_logger`.

**Use f-strings:** `logger.info(f"Results are stored in: {results_path}")` — pylint rule `logging-fstring-interpolation` is disabled (`pyproject.toml:68`).

**Timing pattern — use `mesmo.utils.log_time`:** Wrap any non-trivial block with matched start/end calls that share a label. Two invocations with the same label produce "Starting {label}." followed by "Completed {label} in {seconds} seconds." See `mesmo/utils.py:273-308`.

Canonical usage:

```python
mesmo.utils.log_time("electric grid model instantiation")
self.electric_grid_model = mesmo.electric_grid_models.ElectricGridModel(scenario_name)
mesmo.utils.log_time("electric grid model instantiation")
```

(`mesmo/problems.py:122-124`). Tests use `self._testMethodName` or the literal test name as label and pass `log_level="info", logger_object=logger` — see `tests/test_der_models.py:18,24`.

## Comments

**Style — block comments precede each logical step.**
Every function is decomposed into short labeled blocks, each introduced by a single-line comment in the form `# <Capitalized verb phrase>.` followed by 1–6 lines of code. Example `mesmo/api.py:19-46`:

```python
# Instantiate results directory.
if store_results and (results_path is None):
    results_path = mesmo.utils.get_results_path("run_operation_problem", scenario_name)

# Recreate / overwrite database.
if recreate_database:
    mesmo.data_interface.recreate_database()
```

**When to comment:**

- Always add a `# <verb-phrase>.` header before each logical step of a non-trivial function. This is the dominant in-function documentation style in MESMO.
- Explain non-obvious workarounds with a leading `# -`  bullet, e.g. `# - Suppress numpy runtime warning for divide by zero, because it is expected.` (`mesmo/utils.py:418`).
- Use `# TODO: ...` for known follow-ups. Example `mesmo/config.py:106`: `# TODO: Move physical constants to model definition.` (~20+ TODOs exist across `mesmo/`).

**Docstrings:**

- Google-ish format with `Arguments:`, `Keyword Arguments:`, `Returns:` sections. Sphinx-style `:math:`, `:class:`, `:func:` roles are used for API docs rendered via Sphinx (see `docs/conf.py`).
- Module docstrings are a single line: `"""Database interface."""` (`mesmo/data_interface.py:1`), `"""Utility functions module."""` (`mesmo/utils.py:1`).
- Class docstrings describe purpose, key invariants, and include an `Example:` block with indented literal code (reStructuredText `::` literal block). Canonical example: `ObjectBase` in `mesmo/utils.py:32-84`.
- Function docstrings start with an imperative one-liner, then a dash-bulleted expanded description, then optional `Arguments:` / `Keyword Arguments:` / `Returns:` blocks. See `mesmo/utils.py:log_time` (`273-293`) and `get_plotly_mapbox_zoom_center` (`458-479`).
- Use raw-string docstrings (`r"""..."""`) when the docstring contains LaTeX (backslashes). See `mesmo/solutions.py:OptimizationProblem` at line 20.

## Function Design

**Size:** Functions are pragmatic, not doctrinaire — high-level API functions are ~35 lines (`mesmo/api.py:run_nominal_operation_problem`), utility helpers 5–30 lines, but grid/DER model methods can exceed 100 lines. `too-many-lines` and `too-many-function-args` are explicitly disabled in pylint (`pyproject.toml:72-73`).

**Type hints:**

- **Required on public function signatures** — arguments and return types. See `mesmo/api.py:11-17`:

```python
def run_nominal_operation_problem(
    scenario_name: str,
    recreate_database: bool = True,
    print_results: bool = False,
    store_results: bool = True,
    results_path: str = None,
) -> mesmo.problems.Results:
```

- Use `typing.Union`, `typing.Callable`, `typing.Iterable`, `typing.List`, `typing.Dict` from `typing` rather than PEP 604 `|` syntax.
- Class attributes are declared with type annotations at the top of the class body — this is enforced by `ObjectBase.__setattr__` which emits a warning when an attribute is set without a type-hint declaration (`mesmo/utils.py:32-64`). **Always declare expected attributes at the top of the class.**

**Parameters:**

- Use explicit keyword arguments with defaults for optional parameters (`recreate_database: bool = True`). Avoid `*args` / `**kwargs` except in base-class constructors such as `ResultsBase.__init__` (`mesmo/utils.py:90-93`).
- Use `@multimethod` from the `multimethod` package for dispatch on argument types rather than hand-written `isinstance` ladders. See `mesmo/problems.py:102` and `mesmo/data_interface.py`. Pylint rules `function-redefined` and `no-value-for-parameter` are disabled to support this (`pyproject.toml:67,69`).

**Return values:**

- Return a typed object (a `Results` subclass, a `pd.DataFrame`, a `pathlib.Path`, a tuple of `(float, dict)`). Avoid returning `None` to signal error — raise instead.
- Problem classes follow the contract: `solve()` returns nothing and mutates `self.results`; `get_results() -> Results` returns the structured result. Abstract defaults raise `NotImplementedError` (`mesmo/problems.py:40-44`).

## Module Design

**Exports:**

- The top-level package `mesmo/__init__.py` re-exports every submodule with aliases matching the module name: `import mesmo.api as api`, `import mesmo.utils as utils`, etc. (`mesmo/__init__.py:3-12`). Consumers call `mesmo.api.run_nominal_operation_problem(...)` — never `from mesmo import api`.
- No `__all__` is declared; public surface is anything not prefixed with `_`.

**Barrel files:** Only the package-level `mesmo/__init__.py`. There are no nested packages, so no further `__init__.py` barrel files exist.

**Class attribute declarations:**

- Because `ObjectBase.__setattr__` warns on undeclared attributes, every subclass MUST declare its instance attributes with type hints at the top of the class body. Example `mesmo/der_models.py:23-41`. Treat this as a hard requirement when adding new `ObjectBase` subclasses.

**Results objects:**

- New result surfaces should subclass `mesmo.utils.ResultsBase`, which provides dict-like access (`__getitem__` / `__setitem__`), `.update()`, and `.save()` / `.load()` that auto-serialize `pd.DataFrame`/`pd.Series` to CSV and other types to pickle (`mesmo/utils.py:87-158`).

**Problems objects:**

- New problem classes subclass `mesmo.problems.ProblemBase` and must implement `solve()` and `get_results() -> Results`. The generic test in `tests/test_problems.py` auto-discovers any class in `mesmo.problems` that is not `*Base`, not a `ResultsBase` subclass, and not `*Dict`, then instantiates it with `config["tests"]["scenario_name"]` and calls `.solve()` + `.get_results()`. Ensure new problems accept that single-string constructor signature or they will fail this test.

---

*Convention analysis: 2026-04-20*