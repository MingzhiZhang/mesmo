# Architecture

**Analysis Date:** 2026-04-20

## Pattern Overview

**Overall:** Layered scientific computing library with a "clean architecture" separation between external input (CSV files → SQLite) and internal mathematical models. Python package deployed as a desktop application; all data and dependencies stay local.

**Key Characteristics:**
- Strict three-layer dependency flow: `api` → `problems` → `models` → `data_interface` (+ `utils`/`config`/`solutions` as cross-cutting).
- Model modules never read external input formats directly; they consume `*Data` container objects from `mesmo/data_interface.py`.
- An internal SQLite database (`data/database.sqlite`) is a transient cache populated from CSV inputs on `recreate_database()`.
- Solver-agnostic optimization via the `OptimizationProblem` container in `mesmo/solutions.py` (direct HiGHS, direct Gurobi, and CVXPY fallback).
- Inheritance-based results objects: the `Results` class in `mesmo/problems.py` multiply inherits from per-model `*OperationResults` and `*DLMPResults` classes.
- Optional parallelism via `starmap()` in `mesmo/utils.py`, backed by `multiprocessing` and `ray`.
- CoBMo (building modeling) is a git submodule at `cobmo/` whose `cobmo.building_model` is used only inside `mesmo/der_models.py` for `FlexibleBuildingModel`.

## Layers

**API layer (high-level):**
- Purpose: One-call entry points for end users (system operator / planner) to run canned workflows.
- Location: `mesmo/api.py`
- Contains: `run_nominal_operation_problem()`, `run_optimal_operation_problem()`.
- Depends on: `mesmo.config`, `mesmo.data_interface`, `mesmo.problems`, `mesmo.utils`.
- Used by: Example run scripts under `examples/` (e.g. `examples/run_api_optimal_operation_problem.py`, `examples/run_api_nominal_operation_problem.py`).

**Problem layer (workflow orchestration):**
- Purpose: Sequences model instantiation → solve → result transformation for a full scenario.
- Location: `mesmo/problems.py`
- Contains: `ProblemBase`, `NominalOperationProblem`, `OptimalOperationProblem`, `Results`, `ResultsDict`, `ProblemDict`.
- Depends on: `mesmo.data_interface`, `mesmo.electric_grid_models`, `mesmo.thermal_grid_models`, `mesmo.der_models`, `mesmo.solutions`, `mesmo.utils`.
- Used by: `mesmo/api.py`, researcher scripts, tests in `tests/test_problems.py`.

**Model layer (low-level, mathematical):**
- Purpose: Hold index sets, parameter matrices, and methods to attach variables/constraints/objective onto an `OptimizationProblem`.
- Location: `mesmo/electric_grid_models.py`, `mesmo/thermal_grid_models.py`, `mesmo/der_models.py`.
- Contains:
  - Electric: `ElectricGridModel`, `ElectricGridModelDefault`, `ElectricGridModelOpenDSS`, `PowerFlowSolutionFixedPoint`, `PowerFlowSolutionZBus`, `PowerFlowSolutionOpenDSS`, `PowerFlowSolutionSet`, `LinearElectricGridModelBase`, `LinearElectricGridModelGlobal`, `LinearElectricGridModelLocal`, `LinearElectricGridModelSet`, `ElectricGridOperationResults`, `ElectricGridDLMPResults`.
  - Thermal: `ThermalGridModel`, `ThermalPowerFlowSolutionExplicit`, `ThermalPowerFlowSolutionNewtonRaphson`, `ThermalPowerFlowSolutionSet`, `LinearThermalGridModelGlobal`, `LinearThermalGridModelLocal`, `LinearThermalGridModelSet`, `ThermalGridOperationResults`, `ThermalGridDLMPResults`.
  - DER: `DERModel`, `FixedDERModel`, `FlexibleDERModel`, ten concrete DERs (e.g. `FixedLoadModel`, `FlexibleLoadModel`, `FlexibleEVChargerModel`, `StorageModel`, `FlexibleBuildingModel`, `CoolingPlantModel`, `HeatingPlantModel`, `FlexibleCHP`), `DERModelSet`, factory `make_der_model()`, `make_der_models()`.
- Depends on: `mesmo.data_interface`, `mesmo.solutions`, `mesmo.utils`, `mesmo.config`. `der_models` additionally depends on `cobmo.building_model` and `mesmo.electric_grid_models`. `thermal_grid_models` depends on `mesmo.der_models` for `source_der_model`.
- Used by: `mesmo/problems.py`, tutorial scripts under `examples/tutorial/`.

**Data interface layer:**
- Purpose: Abstract external CSV input from the rest of the codebase; provide typed data containers.
- Location: `mesmo/data_interface.py`, `mesmo/data_schema.sql`
- Contains: `recreate_database()`, `import_csv_file()`, `connect_database()`, `ScenarioData`, `PriceData`, `DERData`, `ElectricGridData`, `ThermalGridData`.
- Depends on: `sqlite3`, `mesmo.config`, `mesmo.utils`, `cobmo.data_interface` (for building data).
- Used by: All `*Model` classes in the model layer; never by the API or problem layers directly.

**Solution layer (solver interface):**
- Purpose: Solver-agnostic convex optimization problem container and solve methods.
- Location: `mesmo/solutions.py`
- Contains: `OptimizationProblem` — manages variables, parameters, linear/quadratic constraints, linear objective, duals; emits LP/QP standard form; dispatches to HiGHS (default), Gurobi, or CVXPY.
- Depends on: `cvxpy`, `gurobipy`, `scipy.sparse`, `mesmo.config`, `mesmo.utils`.
- Used by: `mesmo.problems`, `LinearElectricGridModelSet`, `LinearThermalGridModelSet`, `DERModelSet`, `mesmo.utils.OptimizationProblem` factory (for circular-import-safe construction).

**Visualization layer:**
- Purpose: Results post-processing into figures and animations.
- Location: `mesmo/plots.py`
- Contains: `ElectricGridGraph`, `ThermalGridGraph` (networkx-derived), `create_video()`, and plot functions for line/transformer/node utilization and aggregate time series. Uses `multimethod` for overloaded plot signatures (per-scenario vs. grid-map variants).
- Depends on: `plotly`, `matplotlib`, `networkx`, `cv2` (video), `kaleido`, `mesmo.config`, `mesmo.utils`.
- Used by: Custom user scripts; not called by `api.py` itself (users call it post-solve).

**Cross-cutting — Configuration:**
- Purpose: Central config dictionary, logger factory, parallel-pool lazy instantiation.
- Location: `mesmo/config.py`, `mesmo/config_default.yml`, `config.yml` (auto-created local override, gitignored).
- Contains: `get_config()` (via Dynaconf), `parse_path()`, `get_logger()`, `get_parallel_pool()`. Sets Matplotlib / Plotly / Pandas runtime defaults on import.
- Used by: Every other MESMO module (each calls `mesmo.config.get_logger(__name__)` at module top).

**Cross-cutting — Utilities:**
- Purpose: Base classes, indexing helpers, parallelization, timing, results I/O helpers.
- Location: `mesmo/utils.py`
- Contains: `ObjectBase` (enforces typed attribute declaration), `ResultsBase` (dict-like attribute access + CSV `save()`), `starmap()` (serial / multiprocessing / ray), `chunk_dict`, `chunk_list`, `ray_starmap`, `log_time`, `get_index`, `get_element_phases_array`, `get_element_phases_string`, `get_inverse_with_zeros`, `get_results_path`, `write_figure_plotly`, `launch`, `OptimizationProblem()` (factory to break import cycle).
- Used by: All MESMO modules.

## Data Flow

**Optimal operation problem (primary flow):**

1. User calls `mesmo.api.run_optimal_operation_problem(scenario_name)` in `mesmo/api.py`.
2. `mesmo.data_interface.recreate_database()` rebuilds `data/database.sqlite` from `mesmo/data_schema.sql` plus all CSVs under `data/` and any `additional_data` paths.
3. `OptimalOperationProblem.__init__` in `mesmo/problems.py` instantiates:
   - `ElectricGridModelDefault` (reads `ElectricGridData`), `LinearElectricGridModelSet` (one `LinearElectricGridModel` per timestep, with a reference `PowerFlowSolutionFixedPoint`).
   - `ThermalGridModel` + `LinearThermalGridModelSet` if the scenario has a thermal grid.
   - `DERModelSet` — iterates DER list and calls `make_der_model()`, parallelized via `mesmo.utils.starmap()`; each DER instantiates using `DERData`.
   - An `OptimizationProblem` from `mesmo/solutions.py`.
4. Each model calls its `define_optimization_variables`, `define_optimization_constraints`, `define_optimization_objective` methods, attaching to the shared `OptimizationProblem`.
5. `problem.solve()` → `OptimizationProblem.solve()` emits LP/QP standard form and calls HiGHS, Gurobi, or CVXPY according to `config["optimization"]["solver_name"]`.
6. `problem.get_results()` calls each model's `get_optimization_results()` and `get_optimization_dlmps()`, merges them into a `Results` object, then returns.
7. `results.save(results_path)` writes per-attribute CSVs under `results/<timestamp>_<scenario>/`.

**Nominal operation problem (simulation flow):**

1. `NominalOperationProblem.__init__` loads `ElectricGridModelDefault`, optional `ThermalGridModel`, and `DERModelSet` (fixed DERs only use nominal power time series).
2. `solve()` iterates timesteps: for each, builds a DER nominal power vector and calls `PowerFlowSolutionFixedPoint` (or `PowerFlowSolutionZBus`) in parallel via `starmap()`.
3. `get_results()` unpacks each `PowerFlowSolution` into `Results`.

**State Management:**
- Model objects are immutable after construction; matrices and index sets are built once in `__init__`.
- `Results` / `ResultsBase` are typed-attribute containers; attributes without prior type declaration trigger a warning via `ObjectBase.__setattr__`.
- Parallel pool handle is stored in `mesmo.config.parallel_pool` on first call to `get_parallel_pool()`.
- SQLite connection is returned by `connect_database()` per call; no long-lived global connection.

## Key Abstractions

**`ObjectBase` (in `mesmo/utils.py`):**
- Purpose: Root base for all MESMO model/result classes.
- Examples: `ElectricGridModel`, `ThermalGridModel`, `DERModel`, `PowerFlowSolutionBase`, `OptimizationProblem`.
- Pattern: Template Method + typed attribute contract. All subclasses declare attributes with type hints at class level; setting undeclared attributes emits a warning.

**`ResultsBase` (in `mesmo/utils.py`):**
- Purpose: Dict-like results container with CSV serialization.
- Examples: `ElectricGridDEROperationResults`, `ElectricGridOperationResults`, `ElectricGridDLMPResults`, `ThermalGridOperationResults`, `ThermalGridDLMPResults`, `DERModelOperationResults`, `DERModelSetOperationResults`, and the merged `Results` in `mesmo/problems.py`.
- Pattern: Mixin composition — `Results` multiply inherits from all per-model result classes so a single object aggregates everything.

**`OptimizationProblem` (in `mesmo/solutions.py`):**
- Purpose: Solver-agnostic container for LP/QP in standard form `min cᵀx + ½xᵀQx + d  s.t. Ax ≤ b`.
- Examples: Instantiated inside `OptimalOperationProblem` and passed into `define_optimization_*` methods of `LinearElectricGridModelSet`, `LinearThermalGridModelSet`, `DERModelSet`.
- Pattern: Facade over HiGHS / Gurobi / CVXPY; builds sparse `A`, `b`, `Q`, `c` incrementally via `define_variable`, `define_constraint`, `define_objective`.

**Grid models (`ElectricGridModel` / `ThermalGridModel`):**
- Purpose: Hold index sets (nodes, branches, DERs, phases), admittance / incidence matrices, reference vectors.
- Examples: `ElectricGridModelDefault` (MESMO-native), `ElectricGridModelOpenDSS` (OpenDSS bridge for benchmarking), `ThermalGridModel`.
- Pattern: Abstract base + concrete subclass. Overloaded constructors via `multimethod` accept either a `*Data` object or a `scenario_name`.

**Power flow solutions (`PowerFlowSolutionBase` / `ThermalPowerFlowSolutionBase`):**
- Purpose: Non-linear simulation of a single operating point.
- Examples: `PowerFlowSolutionFixedPoint`, `PowerFlowSolutionZBus`, `PowerFlowSolutionOpenDSS`, `ThermalPowerFlowSolutionExplicit`, `ThermalPowerFlowSolutionNewtonRaphson`.
- Pattern: Strategy — all produce the same output variables (voltage / branch flow / loss vectors) so they are interchangeable in `NominalOperationProblem`. `PowerFlowSolutionSet` wraps a time-series of solutions.

**Linear grid models (`LinearElectricGridModelBase` / `LinearThermalGridModelBase`):**
- Purpose: Sensitivity matrices linking DER power perturbations to nodal voltage / branch flow / losses around a reference `PowerFlowSolution`.
- Examples: `LinearElectricGridModelGlobal`, `LinearElectricGridModelLocal`; `LinearThermalGridModelGlobal`, `LinearThermalGridModelLocal`.
- Pattern: Strategy (global vs. local approximation). `LinearElectricGridModelSet` and `LinearThermalGridModelSet` wrap per-timestep instances and expose the `define_optimization_*` / `get_optimization_results` / `get_optimization_dlmps` protocol.

**DER models (`DERModel`):**
- Purpose: Time-series (fixed) or state-space (flexible) representation of a single distributed energy resource.
- Examples: `FixedLoadModel`, `FixedGeneratorModel`, `FixedEVChargerModel`, `FlexibleLoadModel`, `FlexibleGeneratorModel`, `StorageModel`, `FlexibleEVChargerModel`, `FlexibleBuildingModel`, `CoolingPlantModel`, `HeatingPlantModel`, `FlexibleCHP`.
- Pattern: Two-level abstract hierarchy (`DERModel` → `FixedDERModel` / `FlexibleDERModel` → concrete classes). Created via factory `make_der_model()` that dispatches on `der_type` in `DERData`.

**Data containers (`*Data`):**
- Purpose: Typed snapshot of one scenario's data extracted from SQLite.
- Examples: `ScenarioData`, `PriceData`, `DERData`, `ElectricGridData`, `ThermalGridData`.
- Pattern: Repository — encapsulate SQL queries; return `pd.DataFrame` / `pd.Series` attributes.

## Entry Points

**High-level API:**
- Location: `mesmo/api.py`
- Triggers: User calls `mesmo.api.run_nominal_operation_problem(scenario_name)` or `mesmo.api.run_optimal_operation_problem(scenario_name)`.
- Responsibilities: Recreate DB (optional), instantiate the relevant `*OperationProblem`, call `solve()`, `get_results()`, save CSVs.

**Example scripts:**
- Location: `examples/run_*.py`
- Triggers: `python examples/run_api_optimal_operation_problem.py` etc.
- Responsibilities: Demonstrate the full MESMO workflow; the `run_*.py` scripts are also executed by `tests/test_examples.py` as an integration smoke test.

**Tutorial scripts (low-level workflow):**
- Location: `examples/tutorial/example_1.py`, `example_2.py`, `example_3.py`
- Triggers: Manual execution by researchers.
- Responsibilities: Show how to compose `LinearElectricGridModelSet`, `DERModelSet`, and `OptimizationProblem` directly without the `problems` module.

**Validation scripts:**
- Location: `examples/validation_*.py`
- Triggers: Manual execution or via `tests/test_examples.py`.
- Responsibilities: Cross-check MESMO power flow and linear model outputs against OpenDSS.

**Publication reproducibility scripts:**
- Location: `examples/publications/paper_*.py` and `examples/publications/paper_2021_zhang_distributionally_robust_optimization/`
- Triggers: Manual execution to reproduce paper results; corresponding scenario data lives in `data/test_case_publications/`.

**Development scratchpad:**
- Location: `examples/development/`
- Triggers: Manual; excluded from coverage (see `pyproject.toml` `tool.coverage.report.omit`).

**Unit tests:**
- Location: `tests/test_*.py`
- Triggers: `pytest tests/` or GitHub Actions workflow `.github/workflows/pythontests.yml`.
- Responsibilities: One test module per MESMO module; uses the `singapore_6node` / `singapore_tanjongpagar` scenarios configured in `mesmo/config_default.yml` under `tests:`.

**Install / bootstrap:**
- Location: `development_setup.py`, `setup.py`, `pyproject.toml`
- Triggers: `python development_setup.py` (documented in `README.md`).
- Responsibilities: Install editable MESMO + CoBMo, fetch HiGHS solver binary.

**Module import side-effects:**
- `mesmo/__init__.py` imports all sub-modules. `mesmo/config.py` is initialized first; on import it sets `config` global, Matplotlib / Plotly / Pandas defaults, and writes `./config.yml` if missing.

## Error Handling

**Strategy:** Rely on third-party library exceptions (pandas, scipy, sqlite3, solver SDKs) and log warnings via per-module `logger` objects. No MESMO-specific exception hierarchy.

**Patterns:**
- `ObjectBase.__setattr__` in `mesmo/utils.py` emits `logger.warning` when an undeclared attribute is assigned.
- `get_index()` in `mesmo/utils.py` raises by default on empty indexing but accepts `raise_empty_index_error=False` to return an empty array.
- Solver failures surface as whatever exception the underlying solver raises (e.g., `gurobipy.GurobiError`, `cvxpy.SolverError`).
- Database regeneration is idempotent: `recreate_database()` in `mesmo/data_interface.py` wipes and recreates tables before reloading CSVs.
- Long-running operations are bracketed with `mesmo.utils.log_time(label)` pairs to capture elapsed time on failure.

## Cross-Cutting Concerns

**Logging:**
- Each module gets its own logger via `logger = mesmo.config.get_logger(__name__)` at the top of the file.
- Level set globally by `config["logs"]["level"]` in `mesmo/config_default.yml` (choices: `debug`, `info`, `warn`, `error`). Format is also configurable.
- Timing: `mesmo.utils.log_time(label, log_level, logger_object)` paired calls delimit a timed block; elapsed time written at the second call.

**Validation:**
- Data-level: CSV column names must match SQL table columns in `mesmo/data_schema.sql`; mismatches raise `sqlite3` errors during `import_csv_file()`.
- Class-level: `ObjectBase`'s typed-attribute enforcement catches typos at runtime (warning only).
- No JSON schema / pydantic validation; trust is placed in the CSV → SQL round-trip.

**Authentication:** Not applicable — MESMO is a local desktop library. Gurobi licensing is handled by the `gurobipy` package using the user's environment.

**Parallelization:**
- `mesmo.utils.starmap()` dispatches to `itertools.starmap` (serial), `multiprocessing.Pool.starmap` (CPython), or `ray_starmap` (Ray) based on `config["multiprocessing"]["run_parallel"]` and the presence of Ray.
- Used for independent per-timestep and per-DER work inside `DERModelSet.__init__`, `PowerFlowSolutionSet`, `LinearElectricGridModelSet`, `NominalOperationProblem.solve`.

**Configuration override:** Dynaconf merges `mesmo/config_default.yml` with an optional `config.yml` at the repo root. The file is auto-created on first run by `get_config()` and is listed in `.gitignore`.

**External solver integration:**
- HiGHS is downloaded by `development_setup.py` to `highs/bin/highs` (path set in `mesmo/config_default.yml` under `paths.highs_solver`).
- Gurobi via `gurobipy` (requires license).
- Any CVXPY-supported solver via `solver_interface: cvxpy`.

**OpenDSS integration:** `OpenDSSDirect.py` is used only inside `ElectricGridModelOpenDSS` and `PowerFlowSolutionOpenDSS` in `mesmo/electric_grid_models.py` for power-flow benchmarking.

**CoBMo coupling:** `cobmo/` (git submodule) exposes `cobmo.building_model.BuildingModel`. `mesmo/der_models.py::FlexibleBuildingModel` wraps a CoBMo building as a flexible DER. `mesmo/data_interface.py` imports `cobmo.data_interface` for building-specific CSV ingestion. CoBMo CSVs live under `cobmo/data/`; MESMO's SQLite build intentionally skips any path whose parts contain `cobmo` or `cobmo_data`.

---

*Architecture analysis: 2026-04-20*
