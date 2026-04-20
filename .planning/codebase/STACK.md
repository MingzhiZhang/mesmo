# Technology Stack

**Analysis Date:** 2026-04-20

## Languages

**Primary:**
- Python `>=3.10` - All library code in `mesmo/` and `cobmo/cobmo/`, examples in `examples/`, tests in `tests/`. Version floor enforced in `pyproject.toml`; CI pins `3.10` (`.github/workflows/pythontests.yml`).

**Secondary:**
- SQL (SQLite dialect) - Database schema definitions in `mesmo/data_schema.sql` and `cobmo/cobmo/data_schema.sql`.
- YAML - Configuration files (`mesmo/config_default.yml`, `cobmo/cobmo/config_default.yml`) and conda environment specs (`environment-*.yml`).
- Bash - CI workflow commands in `.github/workflows/*.yml` and Dockerfile `RUN` steps.
- Dockerfile - Container build definition in `Dockerfile`.

## Runtime

**Environment:**
- CPython `3.10` (conda-managed) - Pinned via `environment-*.yml` (`python=3.10.12`); CI uses `conda-incubator/setup-miniconda@v2`; Docker image uses `condaforge/miniforge3:latest` with `python=3.10`.

**Package Manager:**
- `conda` / `mamba` (conda-forge) - Primary install path per `README.md` and `Dockerfile`.
- `pip` - Secondary for non-conda packages and editable installs (`pip install -e .[tests]` via `development_setup.py`).
- Lockfiles: Per-OS conda snapshots present — `environment-macos-latest.yml`, `environment-ubuntu-latest.yml`, `environment-windows-latest.yml`. No `poetry.lock`/`pip-compile` lockfile.

## Frameworks

**Core:**
- `numpy` `1.25.x` - Numerical arrays, linear algebra. Used throughout `mesmo/`.
- `pandas` `2.0.x` - DataFrames for time series, grid data, schedules. Ubiquitous in `mesmo/`.
- `scipy<1.11` - Sparse matrices (`scipy.sparse`), constants, sparse linear solvers. Version cap for CVXPY compatibility (`pyproject.toml`).
- `cvxpy` `1.3.1` - Convex optimization modeling frontend. Used in `mesmo/solutions.py` (`solve_cvxpy`).
- `multimethod` `1.9.x` - Multiple-dispatch decorator for overloaded methods (`mesmo/der_models.py`, `mesmo/electric_grid_models.py`, `mesmo/thermal_grid_models.py`, `mesmo/data_interface.py`, `mesmo/plots.py`).
- `dynaconf` `3.1.x` - Layered YAML configuration loader in `mesmo/config.py` (`get_config`).
- `ray[default]` `2.5.x` - Distributed parallel execution pool via `ray.util.multiprocessing.Pool` in `mesmo/config.py` (`get_parallel_pool`) and `mesmo/utils.py` (`starmap`).

**Testing:**
- `unittest` (stdlib) - Test runner invoked as `python -m unittest discover tests` in `.github/workflows/pythontests.yml`.
- `pytest` - Declared optional dep in `pyproject.toml` `[project.optional-dependencies].tests`; CoBMo also uses `pytest-cov`, `pytest-subtests`.
- `parameterized` - Table-driven tests (optional dep).
- `coverage[toml]` `7.2.x` - Coverage reporting; config in `pyproject.toml` `[tool.coverage.report]`. XML export uploaded to Codecov + Codacy in CI.
- `pylint` `2.17.x` - Linter; config in `pyproject.toml` `[tool.pylint.*]` (max-line-length 120).

**Build/Dev:**
- `setuptools` - Build backend per `pyproject.toml` `[build-system]`; minimal `setup.py` shim for `pip install -e .`.
- `sphinx` + `sphinx-multiversion` + `myst-parser[linkify]` + `furo` + `sphinx-copybutton` + `recommonmark` - Documentation toolchain (`docs/requirements.txt`, `.github/workflows/documentation.yml`).

## Key Dependencies

**Critical:**
- `cvxpy` `1.3.1` - Primary convex optimization modeling layer. `mesmo/solutions.py` imports as `cp` and uses `solve_cvxpy()` path.
- `gurobipy` `10.0.2` - Commercial MIP/LP solver interface; direct native path in `mesmo/solutions.py` (`solve_gurobi`, `get_gurobi_problem`) and alternative solver `option` in `mesmo/config_default.yml`.
- `HiGHS` solver (external binary `highs/bin/highs`) - Default open-source LP/MIP solver. Downloaded by `development_setup.py` from the `JuliaBinaryWrappers/HiGHSstatic_jll.jl` GitHub releases; invoked via `subprocess` in `mesmo/solutions.py` (`solve_highs`).
- `OpenDSSDirect.py` `0.8.3` (`opendssdirect`) - OpenDSS electric distribution simulation engine used in `mesmo/electric_grid_models.py`.
- `cobmo` `0.3.0` - In-tree git submodule (`cobmo/`, source `https://github.com/mesmo-dev/cobmo`) providing building thermal models; imported as `cobmo.building_model`, `cobmo.data_interface`, `cobmo.config` in `mesmo/der_models.py` and `mesmo/data_interface.py`.
- `sqlite3` (stdlib) - Local relational store for grid/DER scenario data; schema `mesmo/data_schema.sql`; connection in `mesmo/data_interface.py` (`recreate_database`).
- `numpy` / `pandas` / `scipy<1.11` - Numerical core, pinned because of CVXPY/OSQP compatibility.

**Infrastructure:**
- `ray` `2.5.1` (`ray[default]`) - Parallel worker pool for CSV import and scenario evaluation.
- `dill` `0.3.6` - Extended pickling (complex objects / closures) for serializing results.
- `tqdm` `4.65.0` - Progress bars in long-running loops.
- `requests` `2.31.x` - Used only by `development_setup.py` to download the HiGHS binary.
- `pyyaml` `6.0` - Loaded via `dynaconf` for the YAML config.
- `natsort` `8.4.x` - Natural sort ordering (node/DER identifiers).
- `networkx` `3.1` - Graph construction for electric grid topology plots (`mesmo/plots.py`).
- `opencv-python-headless` `4.7.x` - Image compositing in grid plots (`import cv2` in `mesmo/plots.py`).

**Plotting / visualization:**
- `matplotlib` `3.7.x` (base) - Static 2D plots, style configured in `mesmo/config.py`.
- `plotly` `5.15.x` (+ `kaleido` `0.2.1` for static export) - Interactive figures in `mesmo/plots.py`.
- `contextily` `1.3.0` (conda-only, optional) - Basemap tiles for georeferenced grid plots; toggled by `plots.add_basemap` in `mesmo/config_default.yml`.
- `bokeh`, `holoviews`, `hvplot`, `panel`, `pvlib`, `psychrolib` - Pulled in transitively by CoBMo (see `cobmo/setup.py`).

## Configuration

**Environment:**
- Layered YAML via `dynaconf`:
  - Defaults: `mesmo/config_default.yml` (paths, optimization, multiprocessing, logs, tests, plots).
  - Overrides: auto-generated `config.yml` in repo base (created on first import by `mesmo/config.py`).
  - CoBMo analog: `cobmo/cobmo/config_default.yml`, merged with MESMO data paths in `mesmo/data_interface.py`.
- Key runtime knobs (`mesmo/config_default.yml`):
  - `optimization.solver_name`: `highs` (default) | `gurobi` | any CVXPY solver (lowercase).
  - `optimization.solver_interface`: `direct` | `cvxpy`.
  - `optimization.time_limit`: seconds (Gurobi/CPLEX only).
  - `multiprocessing.run_parallel` / `multiprocessing.cpu_share`.
  - `logs.level` / `logs.format`.
  - `plots.*` (styles, font, figure size, basemap).
- No `.env` files detected; configuration is file-based only.

**Build:**
- `pyproject.toml` - Project metadata, runtime deps, optional `tests` extra, coverage + pylint config.
- `setup.py` - Stub forwarding to `setuptools` (workaround for editable installs).
- `development_setup.py` - Init submodules, `pip install -e` CoBMo and MESMO `[tests]`, download HiGHS binary. Supports `--highs` flag to reinstall just the solver.
- `Dockerfile` - Conda-forge miniforge base; replicates `development_setup.py` inside the image.

## Platform Requirements

**Development:**
- OS: Linux (Ubuntu), macOS, or Windows — all three are CI matrix targets (`.github/workflows/pythontests.yml`).
- Conda distribution required (Anaconda / Miniconda / Miniforge) per `README.md` installation steps.
- Python 3.10 (minimum; 3.10 used in CI and Docker).
- Submodule checkout (`git submodule update --init --recursive`) for `cobmo/` — `.gitmodules` references `https://github.com/mesmo-dev/cobmo`.
- Optional Gurobi license for commercial solver; otherwise the bundled HiGHS binary is used.
- On Intel CPUs, MKL BLAS recommended (`conda install -c conda-forge "libblas=*=*mkl"` per `README.md`).

**Production:**
- No hosted runtime — MESMO is distributed as a Python library / CLI, not deployed as a service.
- Container path: `Dockerfile` builds a self-contained image from `condaforge/miniforge3:latest`.
- Not currently published to PyPI / conda-forge (`README.md`: "MESMO has not yet been deployed to Python pip / conda package indexes").

---

*Stack analysis: 2026-04-20*
