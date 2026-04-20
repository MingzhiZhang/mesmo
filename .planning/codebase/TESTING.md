# Testing Patterns

**Analysis Date:** 2026-04-20

## Test Framework

**Runner:**
- Python stdlib `unittest` (discovery-based). Declared as a dev dependency in `pyproject.toml:47` (`pytest` is also installed as an optional test dep but not used for test discovery — CI uses `unittest discover`).
- No `unittest`/`pytest` configuration file. There is no `jest.config`-equivalent; tests are found by the default discovery rule `test_*.py` in the `tests/` directory.
- `parameterized` (from the `parameterized` PyPI package) is used for data-driven tests — declared in `pyproject.toml:45`.

**Assertion Library:**
- `unittest.TestCase` assertions only: `self.assertEqual`, `self.assertNotEqual`. No third-party assertion libraries. See `tests/test_template.py:21,33` and `tests/test_data_interface.py:28`.

**Coverage tool:**
- `coverage[toml]` (declared in `pyproject.toml:44`). Config block at `pyproject.toml:53-60`:

```toml
[tool.coverage.report]
include = ["mesmo/*", "examples/*"]
omit = ["examples/development/*"]
```

**Run Commands:**

```bash
# Run all tests (the CI entrypoint — see .github/workflows/pythontests.yml:35)
coverage run -m unittest discover tests

# Produce coverage XML report (CI step)
coverage xml

# Run a single test module
python -m unittest tests.test_api

# Run a single test class or method
python -m unittest tests.test_der_models.TestDERModels.test_storage_model

# Run directly as a script (each test file has the __main__ guard)
python tests/test_api.py
```

No watch-mode or coverage-in-one-step shortcut is defined.

## Test File Organization

**Location:**
- Separate top-level `tests/` directory (NOT co-located with source). Flat layout — one test file per `mesmo/` module.

**Naming:**
- Files: `test_<module_name>.py` — mirrors the source module name. Example: `mesmo/der_models.py` → `tests/test_der_models.py`.
- Classes: `Test<PascalCaseSubject>` — e.g. `TestAPI`, `TestDERModels`, `TestDatabaseInterface`, `TestProblems`, `TestPlots`, `TestExamples`, `TestTemplate`.
- Methods: `test_<snake_case_scenario>` — e.g. `test_run_nominal_operation_problem`, `test_constant_power_model`, `test_connect_database`.

**Structure:**

```
tests/
├── test_api.py                    # Covers mesmo/api.py
├── test_data_interface.py         # Covers mesmo/data_interface.py
├── test_der_models.py             # Covers mesmo/der_models.py
├── test_electric_grid_models.py   # Covers mesmo/electric_grid_models.py
├── test_examples.py               # Runs every examples/*.py as a test
├── test_plots.py                  # Covers mesmo/plots.py
├── test_problems.py               # Auto-discovers & tests all problem classes
├── test_template.py               # Copy-paste template for new test files
└── test_thermal_grid_models.py    # Covers mesmo/thermal_grid_models.py
```

**Template for new test files: copy `tests/test_template.py`.** It shows the canonical imports, logger setup, `log_time` timing wrappers, and `__main__` guard. Rename the class to `Test<Subject>` and replace the sample methods.

## Test Structure

**Canonical test module layout** (enforced by `tests/test_template.py`):

```python
"""Test <subject>."""

import unittest

import mesmo

logger = mesmo.config.get_logger(__name__)


class Test<Subject>(unittest.TestCase):
    def test_<scenario>(self):
        # Obtain test data.
        ...

        # Get result.
        mesmo.utils.log_time("test_<scenario>", log_level="info", logger_object=logger)
        <invoke system under test>
        mesmo.utils.log_time("test_<scenario>", log_level="info", logger_object=logger)

        # Compare expected and actual.  (optional — many tests are smoke tests)
        self.assertEqual(actual, expected)


if __name__ == "__main__":
    unittest.main()
```

**Required elements for every new test file:**
1. Module docstring `"""Test <subject>."""` (one line).
2. `import unittest` + `import mesmo` (no further `from mesmo import ...`; use the full dotted path).
3. Module-level `logger = mesmo.config.get_logger(__name__)`.
4. A single `unittest.TestCase` subclass.
5. Matched pair of `mesmo.utils.log_time(label, log_level="info", logger_object=logger)` calls bracketing the system-under-test invocation in each test method. Use the method name (literal string or `self._testMethodName`) as the label.
6. `if __name__ == "__main__": unittest.main()` guard at the bottom.

**Expected/actual pattern** (`tests/test_template.py:11-21`):

```python
def test_equal(self):
    # Define expected result.
    expected = 4

    # Get actual result.
    mesmo.utils.log_time("test_equal", log_level="info", logger_object=logger)
    actual = 2 + 2
    mesmo.utils.log_time("test_equal", log_level="info", logger_object=logger)

    # Compare expected and actual.
    self.assertEqual(actual, expected)
```

**Patterns:**
- **No setUp / tearDown.** Each test method instantiates its own test data fresh (e.g. `der_data = mesmo.data_interface.DERData(...)` at the top of each `test_*_model` method in `tests/test_der_models.py`).
- **No assertion often acts as "smoke test".** Many tests exercise constructors and `.solve()` / `.get_results()` only to confirm no exception is raised — see `tests/test_api.py`, `tests/test_plots.py`, `tests/test_problems.py`. An uncaught exception fails the test.
- **Parameterized expansion** via `@parameterized.expand(...)` in `tests/test_examples.py:27` and `tests/test_problems.py:27`.

## Mocking

**Framework:** None in use. `unittest.mock` is not imported anywhere in `tests/`.

**Patterns:**
- Tests exercise **real code paths against real data** rather than mocking collaborators. They rely on the bundled SQLite database (built via `mesmo.data_interface.recreate_database()`) and CSV fixtures in `data/`.
- The test scenario name is injected via configuration: `mesmo.config.config["tests"]["scenario_name"]` (defined in `mesmo/config_default.yml`, overridable in local `config.yml`). Every test that needs a scenario reads this value — see `tests/test_data_interface.py:33`, `tests/test_der_models.py:15`, `tests/test_plots.py:14`, `tests/test_problems.py:31`. Override the scenario for local runs by editing `config.yml` at the repo root; do not hard-code scenario names except where the test specifically targets a non-default scenario.

**What to Mock:**
- Nothing by convention. If a true isolation unit test is needed, introduce `unittest.mock` locally — but the project style is integration-first.

**What NOT to Mock:**
- The database, the filesystem, the optimization solver, `ray`, plotly/matplotlib renderers. All are exercised end-to-end.

## Fixtures and Factories

**Test Data:**
- **Scenario-driven.** The default test scenario is declared in `mesmo/config_default.yml` under `tests.scenario_name` and consumed via `mesmo.config.config["tests"]["scenario_name"]` in every scenario-dependent test.
- Some tests hard-code a specific scenario name when the default does not exercise the target feature. Examples: `tests/test_api.py:14` uses `"singapore_tanjongpagar"`; `tests/test_der_models.py:119` uses `"paper_2021_troitzsch_dlmp_scenario_6_7_8"`; `tests/test_plots.py:20` uses `"singapore_tanjongpagar"`.
- DER-type-specific tests pick the **first DER of the matching type** out of the scenario using a `pandas` filter. Example `tests/test_der_models.py:20-23`:

```python
der_data.ders.loc[der_data.ders.loc[:, "der_type"] == "fixed_load", "der_name"].iat[0]
```

Add an inline comment noting that the test fails if no DER of that type is defined in the scenario.

**Location:**
- Real CSV data lives under `data/` (loaded into SQLite on `recreate_database()`). There is no separate `tests/fixtures/` directory.

**Parameterized discovery:**
- `tests/test_problems.py:12-23` enumerates classes in `mesmo.problems` dynamically via `inspect.getmembers`, filtering with `inspect.isclass` and excluding classes ending in `Base`, subclasses of `mesmo.utils.ResultsBase`, the re-exported `multimethod` symbol, and classes ending in `Dict`. Each class is tested via the constructor + `solve()` + `get_results()` contract.
- `tests/test_examples.py:14-21` collects `examples/*.py` (publication scripts are explicitly excluded due to HiGHS solver errors — see TODO comment at `tests/test_examples.py:18-19`). Each example is imported via `importlib.util.spec_from_file_location` and its `main()` is invoked (`tests/test_examples.py:34-39`). **Every example script must expose a `main()` function** or `test_examples` will fail.

## Coverage

**Requirements:** No numeric threshold enforced. CI reports coverage to both Codecov and Codacy (`.github/workflows/pythontests.yml:37-47`), but neither step fails the build (`continue-on-error: true`).

**Included paths** (`pyproject.toml:54-60`):
- `mesmo/*`
- `examples/*` (minus `examples/development/*`)

**View Coverage:**

```bash
coverage run -m unittest discover tests
coverage report          # text summary
coverage xml             # CI-consumable XML
coverage html            # browsable HTML report (open htmlcov/index.html)
```

## Test Types

**Unit Tests:**
- Minimal. `tests/test_template.py` and pure-assertion tests in `tests/test_data_interface.py::test_connect_database` are the only genuine unit tests.

**Integration Tests:**
- The dominant style. Tests instantiate real `mesmo` objects, build the SQLite database, load real scenarios from `data/`, and run real numerical solves. Every file except `test_template.py` is effectively an integration test.

**E2E Tests:**
- `tests/test_examples.py` and `tests/test_problems.py` act as end-to-end tests — they run the full example scripts and problem-class pipelines against real data and real solvers.

**Cross-platform CI:**
- `.github/workflows/pythontests.yml` runs on `windows-latest`, `macos-latest`, and `ubuntu-latest` with Python 3.10, `fail-fast: false`. Each OS has a separate conda env file at `environment-<os>.yml` at the repo root.

## Common Patterns

**Timing wrapper (mandatory for all tests):**

```python
mesmo.utils.log_time("test_storage_model", log_level="info", logger_object=logger)
mesmo.der_models.StorageModel(der_data, ...)
mesmo.utils.log_time("test_storage_model", log_level="info", logger_object=logger)
```

Always bracket the code under test with matched `log_time(label, log_level="info", logger_object=logger)` calls using the same label. The first call logs `Starting {label}.`; the second logs `Completed {label} in N seconds.`. Use either a literal test-method-name string (e.g. `"test_storage_model"`) or `self._testMethodName` (see `tests/test_der_models.py:18,24`).

**Parameterized expansion:**

```python
from parameterized import parameterized

class TestProblems(unittest.TestCase):
    @parameterized.expand(objects)
    def test_problems(self, object_name, object_handle):
        ...
```

Pass a list of `(name, value, ...)` tuples; `parameterized.expand` generates one `test_<method>_<index>_<name>` per tuple. See `tests/test_problems.py:27` and `tests/test_examples.py:26`.

**Async Testing:**
- Not applicable — MESMO has no `async` / `await` code. Parallelism uses `ray` via `mesmo.utils.starmap` and is exercised synchronously from tests.

**Error Testing:**
- No dedicated `self.assertRaises` tests exist. When adding new validation code that raises a specific exception, add an `assertRaises` test using this idiom:

```python
with self.assertRaises(ValueError):
    mesmo.<module>.<func>(<invalid input>)
```

**Type-based equality assertion:**

```python
def test_connect_database(self):
    expected = sqlite3.dbapi2.Connection
    actual = type(mesmo.data_interface.connect_database())
    self.assertEqual(actual, expected)
```

(`tests/test_data_interface.py:18-28`). Compare `type(obj)` to the expected class when validating constructor wiring. Use this sparingly — prefer `self.assertIsInstance(obj, Expected)` for subclass-friendly checks (note: not currently used in MESMO, but compatible with the `unittest` style).

---

*Testing analysis: 2026-04-20*
