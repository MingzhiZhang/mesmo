# Codebase Structure

**Analysis Date:** 2026-04-20

## Directory Layout

```
mesmo/
├── mesmo/                              # Core Python package (the library itself)
│   ├── __init__.py                     # Re-exports all sub-modules
│   ├── api.py                          # High-level entry points
│   ├── config.py                       # Dynaconf-backed settings & logger factory
│   ├── config_default.yml              # Default configuration values
│   ├── data_interface.py               # CSV → SQLite ingestion + `*Data` containers
│   ├── data_schema.sql                 # SQL schema for the internal SQLite DB
│   ├── der_models.py                   # DER model classes + factory
│   ├── electric_grid_models.py         # Electric grid / power flow / linear models
│   ├── thermal_grid_models.py          # Thermal grid / power flow / linear models
│   ├── problems.py                     # NominalOperationProblem, OptimalOperationProblem, Results
│   ├── solutions.py                    # OptimizationProblem (solver-agnostic LP/QP)
│   ├── plots.py                        # Plotly/matplotlib result visualizations
│   └── utils.py                        # ObjectBase, ResultsBase, starmap, indexing helpers
├── cobmo/                              # Git submodule: CoBMo (building modeling)
│   ├── cobmo/                          # CoBMo Python package
│   │   ├── __init__.py
│   │   ├── building_model.py           # Used by mesmo.der_models.FlexibleBuildingModel
│   │   ├── config.py
│   │   ├── data_interface.py           # Used by mesmo.data_interface
│   │   ├── data_schema.sql
│   │   ├── plots.py
│   │   └── utils.py
│   ├── data/                           # CoBMo building CSV test data
│   └── examples/, docs/, tests/        # CoBMo's own examples/docs/tests
├── data/                               # Scenario and library CSVs (input format)
│   ├── templates/                      # Empty-schema CSV templates for all tables
│   ├── library/                        # Reusable library entries (line types, schedules, etc.)
│   ├── test_case_examples/             # Example grids: ieee_4node, ieee_34node, ieee_123node,
│   │                                   #  test_2node, tutorial_example, singapore_6node,
│   │                                   #  singapore_tanjongpagar
│   ├── test_case_publications/         # Data to reproduce published papers
│   ├── test_case_development/          # Work-in-progress scenarios (e.g. primo_survey)
│   ├── cobmo/                          # Building-model CSVs consumed by CoBMo
│   └── database.sqlite                 # Generated cache (gitignored)
├── examples/                           # Runnable scripts demonstrating MESMO usage
│   ├── run_api_nominal_operation_problem.py
│   ├── run_api_optimal_operation_problem.py
│   ├── run_electric_grid_optimal_operation.py
│   ├── run_thermal_grid_optimal_operation.py
│   ├── run_multi_grid_optimal_operation.py
│   ├── run_flexible_der_optimal_operation.py
│   ├── run_general_optimization_problem.py
│   ├── validation_*.py                 # MESMO-vs-OpenDSS cross-checks
│   ├── tutorial/                       # Tutorial examples referenced in docs
│   ├── publications/                   # Paper reproduction scripts
│   └── development/                    # Work-in-progress scripts (excluded from coverage)
├── tests/                              # One pytest module per MESMO module
│   ├── test_api.py
│   ├── test_data_interface.py
│   ├── test_der_models.py
│   ├── test_electric_grid_models.py
│   ├── test_examples.py
│   ├── test_plots.py
│   ├── test_problems.py
│   ├── test_thermal_grid_models.py
│   └── test_template.py
├── docs/                               # Sphinx-based documentation (published to GitHub Pages)
│   ├── README.md, index.md
│   ├── architecture.md                 # Authoritative architecture reference
│   ├── api_reference.md
│   ├── configuration_reference.md
│   ├── data_reference.md
│   ├── examples.md
│   ├── installation.md
│   ├── contributing.md
│   ├── change_log.md
│   ├── publications.md
│   ├── conf.py                         # Sphinx conf (lists autodoc_mock_imports)
│   ├── requirements.txt                # Docs-only deps
│   ├── assets/, static/, templates/    # Images, CSS, nav templates
├── results/                            # Default output directory (gitignored)
├── .github/
│   └── workflows/                      # GitHub Actions (pythontests, documentation)
├── .planning/
│   └── codebase/                       # GSD codebase-mapping artifacts (this file)
├── .understand-anything/               # Tool-managed knowledge graph artifacts
├── README.md                           # Project overview + install
├── LICENSE                             # MIT
├── CITATION.bib                        # Zenodo citation
├── Dockerfile                          # Container build recipe
├── pyproject.toml                      # Project metadata, dependencies, pylint, coverage
├── setup.py                            # Legacy setup shim (still required for CoBMo-style install)
├── development_setup.py                # Installs editable MESMO+CoBMo and fetches HiGHS
├── environment-{ubuntu,macos,windows}-latest.yml   # Conda environment specs
├── .gitignore
├── .gitmodules                         # Declares the `cobmo` submodule
└── Multi-Energy System Modeling and Optimization (MESMO).pdf   # Upstream paper
```

## Directory Purposes

**`mesmo/`:**
- Purpose: The MESMO Python package — the only code shipped via `pip install .`.
- Contains: Exactly one `.py` file per module (no sub-packages). Plus YAML default config (`config_default.yml`) and SQL schema (`data_schema.sql`).
- Key files: `api.py`, `problems.py`, `electric_grid_models.py`, `thermal_grid_models.py`, `der_models.py`, `data_interface.py`, `solutions.py`, `utils.py`, `config.py`, `plots.py`.

**`cobmo/`:**
- Purpose: Git submodule hosting the CoBMo (Control-oriented Building Model) package used by `mesmo.der_models.FlexibleBuildingModel`.
- Contains: An independent Python package (`cobmo/cobmo/`) with its own data schema, plus CoBMo's own `data/`, `docs/`, `tests/`, `examples/`.
- Key files: `cobmo/cobmo/building_model.py`, `cobmo/cobmo/data_interface.py`, `cobmo/cobmo/data_schema.sql`.
- Committed: Yes (as a submodule pointer).

**`data/`:**
- Purpose: CSV input data for scenarios and reusable library items. All CSVs are loaded into the internal SQLite DB by `mesmo.data_interface.recreate_database()`.
- Contains: Sub-directories per test case (`test_case_examples/<scenario_name>/*.csv`, `test_case_publications/paper_*/…`, `test_case_development/…`), plus `library/` (shared line/DER/price definitions) and `templates/` (empty-row headers for each table).
- Key files: `data/test_case_examples/singapore_6node/scenarios.csv`, `data/templates/scenarios.csv`, `data/library/electric_grid_line_types.csv`, `data/library/der_models.csv`.
- Special: `data/database.sqlite` is generated at first run and is gitignored. `data/cobmo/` hosts CoBMo-format building CSVs and is explicitly excluded from MESMO's CSV sweep in `mesmo.data_interface.recreate_database()`.

**`examples/`:**
- Purpose: Primary onboarding surface — every `run_*.py` is a self-contained demonstration of a workflow.
- Contains: Top-level `run_*.py` (high-level API) and `validation_*.py` (benchmarking vs. OpenDSS), plus three sub-directories: `tutorial/` (numbered examples referenced in docs), `publications/` (paper reproduction), `development/` (scratchpad, omitted from coverage).
- Key files: `examples/run_api_optimal_operation_problem.py`, `examples/tutorial/example_1.py`, `examples/run_general_optimization_problem.py`.

**`tests/`:**
- Purpose: unittest-style tests executed by pytest, one module per MESMO module.
- Contains: `test_api.py`, `test_data_interface.py`, `test_der_models.py`, `test_electric_grid_models.py`, `test_examples.py`, `test_plots.py`, `test_problems.py`, `test_thermal_grid_models.py`, `test_template.py`.
- Key files: `tests/test_template.py` (pattern template for new test modules).

**`docs/`:**
- Purpose: Sphinx documentation source; built by GitHub Actions and published to `mesmo-dev.github.io/mesmo`.
- Contains: Markdown content (`*.md`), `conf.py` (Sphinx config with `autodoc_mock_imports`), `requirements.txt` (doc-only deps), `assets/` (images), `static/css/`, `templates/`.
- Key files: `docs/architecture.md` (authoritative architecture description), `docs/api_reference.md`, `docs/data_reference.md`, `docs/conf.py`.

**`results/`:**
- Purpose: Default output directory where `Results.save()` writes CSVs and figures.
- Generated: Yes. Committed: No (gitignored).

**`.github/workflows/`:**
- Purpose: CI automation — test matrix across OSes, docs build, release.
- Key files: `.github/workflows/pythontests.yml` (referenced from README badges).

**`.planning/codebase/`:**
- Purpose: GSD mapping artifacts (this document and siblings).
- Contains: `ARCHITECTURE.md`, `STRUCTURE.md`, and whichever other focus docs are generated.
- Committed: Typically yes (project choice).

## Key File Locations

**Entry Points:**
- `mesmo/api.py`: High-level `run_nominal_operation_problem()` / `run_optimal_operation_problem()`.
- `examples/run_api_optimal_operation_problem.py`: Shortest user-facing example.
- `examples/tutorial/example_1.py`: Low-level workflow (manual composition of `LinearElectricGridModelSet`, `DERModelSet`, `OptimizationProblem`).
- `development_setup.py`: Bootstrap installer (MESMO editable + CoBMo + HiGHS).

**Configuration:**
- `mesmo/config_default.yml`: Committed defaults (paths, solver, multiprocessing, logs, tests, plots).
- `config.yml`: Local override at repo root, auto-created on first `mesmo.config.get_config()` call, gitignored.
- `pyproject.toml`: Project metadata, runtime + test dependencies, pylint config, coverage config.
- `environment-{ubuntu,macos,windows}-latest.yml`: Conda environment per OS.
- `Dockerfile`: Container build recipe.

**Core Logic (models):**
- `mesmo/electric_grid_models.py`: `ElectricGridModelDefault`, `ElectricGridModelOpenDSS`, `PowerFlowSolutionFixedPoint`, `PowerFlowSolutionZBus`, `PowerFlowSolutionOpenDSS`, `LinearElectricGridModelGlobal`, `LinearElectricGridModelLocal`, `LinearElectricGridModelSet`.
- `mesmo/thermal_grid_models.py`: `ThermalGridModel`, `ThermalPowerFlowSolutionExplicit`, `ThermalPowerFlowSolutionNewtonRaphson`, `LinearThermalGridModelGlobal`, `LinearThermalGridModelLocal`, `LinearThermalGridModelSet`.
- `mesmo/der_models.py`: `DERModel`, `FixedDERModel`, `FlexibleDERModel`, concrete DER subclasses, `DERModelSet`, `make_der_model()`.
- `mesmo/problems.py`: `NominalOperationProblem`, `OptimalOperationProblem`, `Results`.
- `mesmo/solutions.py`: `OptimizationProblem`.

**Data access:**
- `mesmo/data_interface.py`: `recreate_database()`, `connect_database()`, `ScenarioData`, `PriceData`, `DERData`, `ElectricGridData`, `ThermalGridData`.
- `mesmo/data_schema.sql`: Full SQLite schema (one CREATE TABLE per CSV).

**Testing:**
- `tests/test_template.py`: Boilerplate for new test modules.
- `tests/test_api.py`: Covers the public API functions.
- `tests/test_examples.py`: Runs the `examples/run_*.py` scripts as smoke tests.
- `mesmo/config_default.yml` under the `tests:` key selects the default scenarios (`singapore_6node`, `singapore_tanjongpagar`).

**Submodule bridge:**
- `cobmo/cobmo/building_model.py`: Imported in `mesmo/der_models.py` as `import cobmo.building_model` for `FlexibleBuildingModel`.
- `cobmo/cobmo/data_interface.py`: Imported in `mesmo/data_interface.py`.

## Naming Conventions

**Files:**
- Pattern: `snake_case.py`. Examples: `electric_grid_models.py`, `thermal_grid_models.py`, `der_models.py`, `data_interface.py`.
- Plural for module names that host multiple related classes (`..._models.py`, `problems.py`, `solutions.py`).
- Test files: `test_<module_name>.py` — one file per MESMO module.
- Example files: `run_<what_it_runs>.py` and `validation_<what_it_validates>.py` at `examples/` root; `example_<N>.py` under `examples/tutorial/`; `paper_<year>_<firstauthor>_<topic>.py` under `examples/publications/`.
- CSV files: `snake_case.csv` matching SQL table names exactly (enforced by `mesmo.data_interface.import_csv_file` which uses the filename as table name).

**Directories:**
- Pattern: `snake_case` throughout — e.g. `test_case_examples`, `singapore_tanjongpagar`, `paper_2021_zhang_distributionally_robust_optimization`.
- Scenario directories under `data/test_case_examples/<scenario_name>/` match the `scenario_name` string used in code.

**Classes:**
- `PascalCase`. Bases/abstract: `*Base` suffix (`ProblemBase`, `PowerFlowSolutionBase`, `LinearElectricGridModelBase`).
- Concrete subclasses embed the variant: `PowerFlowSolutionFixedPoint`, `LinearElectricGridModelGlobal`, `FixedLoadModel`.
- Result containers: `*Results` suffix (`ElectricGridOperationResults`, `ThermalGridDLMPResults`, `DERModelSetOperationResults`).
- Data containers: `*Data` suffix (`ElectricGridData`, `DERData`, `ScenarioData`).
- Collection/set wrappers: `*Set` suffix (`DERModelSet`, `LinearElectricGridModelSet`, `PowerFlowSolutionSet`).

**Functions and variables:**
- `snake_case` for module-level functions, methods, and variables.
- Factory functions: `make_<thing>()` (`make_der_model`, `make_der_models`).
- Getter-style module helpers: `get_<thing>()` (`get_config`, `get_logger`, `get_index`, `get_results_path`).
- Private helpers inside modules are **not** prefixed with underscore by convention (the codebase uses explicit imports instead of wildcard).

## Where to Add New Code

**New DER type:**
- Primary code: Add a subclass of `FlexibleDERModel` or `FixedDERModel` in `mesmo/der_models.py`; extend the `if der.at["der_type"] == "..."` dispatch in `make_der_model()`.
- Data: Extend `mesmo/data_schema.sql` with any new DER-specific table; add a template CSV to `data/templates/` and at least one example row under `data/test_case_examples/.../`.
- Tests: Add a test case in `tests/test_der_models.py`.

**New power flow or linear grid variant (electric):**
- Primary code: Subclass `PowerFlowSolutionBase` or `LinearElectricGridModelBase` in `mesmo/electric_grid_models.py`.
- Wire-up: If it needs to be used by `OptimalOperationProblem`, expose it through `LinearElectricGridModelSet`.
- Tests: `tests/test_electric_grid_models.py`.

**New power flow or linear grid variant (thermal):**
- Same pattern as electric, but in `mesmo/thermal_grid_models.py` and `tests/test_thermal_grid_models.py`.

**New problem type:**
- Primary code: Subclass `ProblemBase` in `mesmo/problems.py` and implement `solve()` + `get_results()`.
- API surface (optional): Add a `run_<problem>_problem` wrapper in `mesmo/api.py`.
- Tests: `tests/test_problems.py`.

**New data container:**
- Primary code: Add a `*Data` subclass of `mesmo.utils.ObjectBase` in `mesmo/data_interface.py`; have it use `connect_database()` and return `pd.DataFrame` attributes.
- Schema: Update `mesmo/data_schema.sql` for any new tables.
- Tests: `tests/test_data_interface.py`.

**New solver integration:**
- Primary code: Add a branch in `OptimizationProblem.solve` / helper methods in `mesmo/solutions.py`. Follow the existing HiGHS / Gurobi / CVXPY pattern.
- Config: Document the solver name in `mesmo/config_default.yml` and `docs/configuration_reference.md`.

**New plot type:**
- Primary code: Add a function in `mesmo/plots.py`. Use `@multimethod.multimethod` if overloading by input type, and standardize on `plotly` for interactive output + `mesmo.utils.write_figure_plotly` for file output.
- Tests: `tests/test_plots.py`.

**New utility (cross-cutting helper):**
- Primary code: Add to `mesmo/utils.py`. Do not create a new module for a handful of helpers — MESMO is flat-by-design (no sub-packages).

**New example / tutorial:**
- Primary code: `examples/run_<name>.py` for high-level; `examples/tutorial/example_<N>.py` for pedagogical flow; `examples/development/` for scratch work (omitted from coverage per `pyproject.toml`).

**New scenario data:**
- Under `data/test_case_examples/<scenario_name>/`, copy structure from an existing scenario (e.g. `singapore_6node/`). All CSVs are auto-discovered by `mesmo.data_interface.recreate_database()`.

**New documentation page:**
- Add a Markdown file under `docs/` and link it from `docs/index.md`. Sphinx conf is at `docs/conf.py`.

**New dependency:**
- Add to `pyproject.toml` under `[project] dependencies` (or `[project.optional-dependencies]`). Also add it to `autodoc_mock_imports` in `docs/conf.py` per the note in `pyproject.toml`. Update `environment-*-latest.yml` conda files if the dependency is conda-provided.

## Special Directories

**`cobmo/`:**
- Purpose: Git submodule for the CoBMo building-modeling package.
- Generated: No.
- Committed: Yes (submodule pointer in `.gitmodules`).
- Note: Skipped during MESMO's CSV scan — `mesmo.data_interface.recreate_database()` excludes any path whose parts contain `cobmo` or `cobmo_data`.

**`data/database.sqlite`:**
- Purpose: Transient cache rebuilt from CSVs.
- Generated: Yes, by `mesmo.data_interface.recreate_database()`.
- Committed: No (gitignored).

**`results/`:**
- Purpose: Default location for solver results (timestamped sub-directories).
- Generated: Yes, by `mesmo.utils.get_results_path()`.
- Committed: No (gitignored).

**`config.yml` (repo root):**
- Purpose: Local configuration override for `mesmo/config_default.yml`.
- Generated: Yes, auto-created by `mesmo.config.get_config()` on first run.
- Committed: No (gitignored).

**`highs/`:**
- Purpose: Default location where `development_setup.py` unpacks the HiGHS solver binary (`highs/bin/highs`, referenced in `mesmo/config_default.yml`).
- Generated: Yes (by installer).
- Committed: No.

**`examples/development/`:**
- Purpose: Work-in-progress scripts.
- Generated: No.
- Committed: Yes, but explicitly excluded from coverage reports in `pyproject.toml` (`tool.coverage.report.omit`).

**`.understand-anything/`:**
- Purpose: Artifacts from the Understand-Anything knowledge graph tooling (not part of MESMO).
- Generated: Yes.
- Committed: Project-dependent; typically not relevant to MESMO's functionality.

**`.planning/`:**
- Purpose: GSD workflow artifacts (codebase maps, phase plans, etc.).
- Generated: Yes, by GSD commands.
- Committed: Project choice.

---

*Structure analysis: 2026-04-20*
