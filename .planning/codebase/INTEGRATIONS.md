# External Integrations

**Analysis Date:** 2026-04-20

## APIs & External Services

**Optimization solvers (third-party numerical engines):**
- HiGHS (open-source LP/MIP) - Default solver. Invoked as an external CLI binary via `subprocess` from `mesmo/solutions.py` (`solve_highs`). Binary path configured at `optimization.highs_solver` (default `./highs/bin/highs` in `mesmo/config_default.yml`). Downloaded from the `JuliaBinaryWrappers/HiGHSstatic_jll.jl` GitHub releases by `development_setup.py`.
  - SDK/Client: None (CLI subprocess, reads/writes standard LP files).
  - Auth: None (local binary).
- Gurobi (commercial MIP/LP) - Optional solver with direct native interface. Imported as `gurobipy as gp` in `mesmo/solutions.py`; used in `get_gurobi_problem()` / `solve_gurobi()`.
  - SDK/Client: `gurobipy==10.0.2`.
  - Auth: Gurobi license file (WLS / named-user / academic) resolved at runtime by the `gurobipy` library; not managed by MESMO code. No env-var indirection in-repo.
- CVXPY-supported backends (ECOS, SCS, OSQP, MOSEK, CPLEX, …) - Accessed through `cvxpy` when `optimization.solver_interface = cvxpy`. `mesmo/solutions.py` builds the CVXPY `Problem`; selection follows `optimization.solver_name`.
  - SDK/Client: `cvxpy==1.3.1`, plus per-backend packages pulled in by conda env (`ecos`, `osqp`, `scs`).
  - Auth: Only CPLEX/MOSEK need licenses; not wired up in code.

**Power-system simulation engine:**
- OpenDSS (EPRI distribution system simulator) - Non-linear power flow / steady-state analysis backend for electric grids.
  - SDK/Client: `OpenDSSDirect.py==0.8.3` (module `opendssdirect`, ships with `dss-python==0.14.3` + `dss-python-backend==0.13.3` binaries). Imported in `mesmo/electric_grid_models.py`.
  - Auth: None (in-process native library).

**HTTP downloads (one-shot during setup):**
- GitHub Releases (`github.com/JuliaBinaryWrappers/HiGHSstatic_jll.jl`) - Source of the HiGHS solver archive. Downloaded via `requests.get(..., stream=True)` in `development_setup.py`; platform-specific tarball chosen by `sys.platform`.
  - SDK/Client: `requests==2.31.0`.
  - Auth: None (public release assets).

No other outbound API integrations (no REST clients, no SaaS SDKs, no cloud provider SDKs) are used at runtime.

## Data Storage

**Databases:**
- SQLite (embedded, file-backed) - Only persistent store. Single database file whose path is set by `paths.database` (default `./data/database.sqlite` in `mesmo/config_default.yml`).
  - Connection: `sqlite3.connect(...)` in `mesmo/data_interface.py` (`recreate_database`).
  - Client: `sqlite3` (Python stdlib); DataFrame I/O via `pandas.read_sql`.
  - Schema: DDL in `mesmo/data_schema.sql` (tables for DERs, grid definitions, schedules, etc.). CoBMo has its own schema at `cobmo/cobmo/data_schema.sql`, loaded by `cobmo.data_interface.recreate_database()`.
  - Source data: CSV files discovered recursively under `paths.data` and `paths.additional_data`; imported into SQLite by `mesmo.data_interface.import_csv_file` on `recreate_database()`.

**File Storage:**
- Local filesystem only:
  - `paths.data` (default `./data`) - Input CSV datasets + scenario definitions.
  - `paths.additional_data` / `paths.cobmo_additional_data` - Extra user-supplied CSV roots (YAML list).
  - `paths.results` (default `./results`) - Output directory for run artifacts; path helper in `mesmo/utils.py` (`get_results_path`); results serialized by `mesmo/solutions.py` `Results.save()` and referenced in `mesmo/api.py`.
  - `paths.highs_solver` (default `./highs/bin/highs`) - Installed HiGHS binary.

**Caching:**
- None. No in-memory cache layer, no Redis/Memcached. Config is loaded once at import time by `dynaconf` in `mesmo/config.py`.

## Authentication & Identity

**Auth Provider:**
- Not applicable - MESMO is a Python library / CLI with no user sessions, multi-tenancy, or network-exposed surface. No login, OAuth, JWT, or RBAC code in the repo.
- The only credential-bearing external dependency is the optional Gurobi license, handled entirely by `gurobipy` outside MESMO.

## Monitoring & Observability

**Error Tracking:**
- None. No Sentry, Rollbar, Datadog, OpenTelemetry, or equivalent client is imported. Errors surface via Python exceptions and log output.

**Logs:**
- Python stdlib `logging` via `mesmo.config.get_logger(name)` (`mesmo/config.py`).
- Single stream handler writing to stderr, format and level driven by `logs.format` and `logs.level` in `mesmo/config_default.yml` (`debug` / `info` / `warn` / `error`).
- Timing helper `mesmo.utils.log_time` wraps named blocks (used throughout `mesmo/data_interface.py`).
- No structured logging, no log shipping.

**Metrics / tracing:**
- None. `ray` workers are local only; Ray Dashboard is available via `ray[default]` but not wired into any product telemetry.

## CI/CD & Deployment

**Hosting:**
- Documentation is published to GitHub Pages at `mesmo-dev.github.io/mesmo` (`.github/workflows/documentation.yml`, deploy via `peaceiris/actions-gh-pages@v3`).
- No application hosting (the project ships as a library).

**CI Pipeline (GitHub Actions):**
- `.github/workflows/pythontests.yml` - Matrix (`windows-latest`, `macos-latest`, `ubuntu-latest`) × Python 3.10. Steps: checkout with `submodules: recursive`, `conda-incubator/setup-miniconda@v2`, `conda create` + `python development_setup.py`, run `coverage run -m unittest discover tests`, then `coverage xml`. Coverage uploaded to:
  - Codecov (`codecov/codecov-action@v2`, no token — public repo).
  - Codacy (`codacy/codacy-coverage-reporter-action@v1`, reads `secrets.CODACY_PROJECT_TOKEN`).
- `.github/workflows/documentation.yml` - Builds Sphinx (multi-version) on the `develop` branch and deploys to `gh-pages`. Uses `secrets.GITHUB_TOKEN`.
- `.github/workflows/maintenance.yml` - Additional maintenance workflow (not inspected in detail).

**Container build:**
- `Dockerfile` - Produces a conda-based image (`condaforge/miniforge3:latest`); not pushed to a registry from CI in the workflows examined.

## Environment Configuration

**Required env vars:**
- None required for normal runtime. MESMO reads all configuration from YAML (`mesmo/config_default.yml` + optional `config.yml`), not from `os.environ`.
- CI-only secrets (not used at runtime):
  - `CODACY_PROJECT_TOKEN` - Coverage reporter in `.github/workflows/pythontests.yml`.
  - `GITHUB_TOKEN` - Auto-provided, used in `.github/workflows/documentation.yml`.

**Secrets location:**
- GitHub Actions repository secrets only (referenced as `${{ secrets.* }}`).
- No `.env`, no `.env.*`, no `credentials.*` files present in the repository.
- Gurobi license (if used) is resolved by the `gurobipy` library from its own standard locations (e.g., `GRB_LICENSE_FILE`) — not touched by MESMO code.

## Webhooks & Callbacks

**Incoming:**
- None. MESMO does not expose any HTTP/WebSocket endpoints, server processes, or listener sockets.

**Outgoing:**
- None at runtime. The sole outbound HTTP call is the one-shot HiGHS binary download in `development_setup.py` (GitHub Releases); no scheduled callbacks, no webhooks.

---

*Integration audit: 2026-04-20*
