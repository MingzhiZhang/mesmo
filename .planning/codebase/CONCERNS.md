# Codebase Concerns

**Analysis Date:** 2026-04-20

## Tech Debt

**Pervasive `TODO` markers across modeling modules:**
- Issue: 60+ `TODO` comments spread across core modules flag unfinished work, missing validation, undocumented parameters, and hard-coded workarounds. No tracker ticket associations.
- Files:
  - `mesmo/electric_grid_models.py` — 35+ TODOs (most concentrated; includes unvalidated models, missing delta-connection handling, sign-change documentation gaps)
  - `mesmo/der_models.py` — 14+ TODOs (shifting losses / self-discharge consistently deferred across multiple storage/battery classes, "CHP cost defined twice" bug flag)
  - `mesmo/thermal_grid_models.py` — 9+ TODOs (pump power sensitivity equation acknowledged wrong at `mesmo/thermal_grid_models.py:741` and `mesmo/thermal_grid_models.py:974`)
  - `mesmo/solutions.py:348,462,711,1016,1379` — deferred error handling ("TODO: Raise error if ...")
  - `mesmo/problems.py:170,204,524,541,823,843,848,863` — trust-region algorithm has acknowledged logic gaps
  - `mesmo/data_interface.py:605` — silent data overwrite ("`.fillna(0.0)` — This overwrites any missing values. No warning is raised.")
- Impact: Hidden correctness risks (wrong pump sensitivities, undocumented sign conventions, silent NaN → 0 coercion), blocks production readiness, makes future changes risky.
- Fix approach: Triage all TODOs → convert to issues in tracker. Prioritize correctness TODOs (pump sensitivity, CHP double-costing, DLMP single-phase gap) over documentation TODOs.

**Deprecated backwards-compatibility placeholders:**
- Issue: `ElectricGridModelDefault` (`mesmo/electric_grid_models.py:877`) and `mesmo.utils.OptimizationProblem()` (`mesmo/utils.py:570`) are placeholder classes that log a warning on every instantiation. No deprecation timeline is recorded.
- Files: `mesmo/electric_grid_models.py:877-889`, `mesmo/utils.py:570-584`
- Impact: Dead code paths held open indefinitely; creates ambiguity about the supported API surface.
- Fix approach: Set a removal version in `pyproject.toml` version bump notes; replace `logger.warning` with `DeprecationWarning` via `warnings.warn` so downstream callers can filter them; remove after one release cycle.

**Commented-out code retained:**
- Issue: Large commented-out blocks kept inline instead of versioned. Examples: dead `multiprocessing.Pool` bootstrap at `mesmo/utils.py:182-189`, commented-out trust-region "line flow violation" block at `mesmo/problems.py:823-831,863-870`.
- Files: `mesmo/utils.py`, `mesmo/problems.py`
- Impact: Clutters logic; readers cannot tell whether the commented branch is a known-good alternative or abandoned code.
- Fix approach: Remove or move to design notes; git history preserves them.

**Hard-coded physical constants at module scope:**
- Issue: Water density, kinematic viscosity, gravitational acceleration live at module scope with a `TODO: Move physical constants to model definition` (`mesmo/config.py:105-109`).
- Files: `mesmo/config.py:106-109`
- Impact: Violates "model-owns-its-parameters"; cannot simulate non-water coolant or non-Earth scenarios without monkey-patching the config module.
- Fix approach: Add a `PhysicalConstants` dataclass (or pull from `thermal_grid` scenario parameters) and thread it through `ThermalGridModel.__init__`.

**Very large modules (cohesion risk):**
- Issue: Core modeling files exceed 1000 lines; `mesmo/electric_grid_models.py` is 4546 lines with the `too-many-lines` pylint rule explicitly disabled in `pyproject.toml:73`.
- Files:
  - `mesmo/electric_grid_models.py` (4546 lines)
  - `mesmo/der_models.py` (2403 lines)
  - `mesmo/thermal_grid_models.py` (1499 lines)
  - `mesmo/solutions.py` (1451 lines)
  - `mesmo/plots.py` (1307 lines)
- Impact: Slow IDE navigation, high merge-conflict surface, cognitive overhead when modifying a single model class.
- Fix approach: Split `electric_grid_models.py` by class — move `ElectricGridModelOpenDSS`, `PowerFlowSolutionFixedPoint`, `LinearElectricGridModel*`, and DLMP calculators into submodules.

**`# Note: Dependencies must also be added in `docs/conf.py` to `autodoc_mock_imports`` (`pyproject.toml:19`):**
- Issue: Manual sync required between `pyproject.toml` dependencies and Sphinx mock imports.
- Files: `pyproject.toml:19-20`, `docs/conf.py`
- Impact: Easy to forget; docs build breaks silently on new deps.
- Fix approach: Auto-generate `autodoc_mock_imports` from `project.dependencies` in `docs/conf.py`.

## Known Bugs

**Trust-region solver can loop to iteration limit with oscillating sigma:**
- Symptoms: "there are cases when sigma repeats itself every second iteration causing an endless loop until the max number of iterations is reached" — flagged in source.
- Files: `mesmo/problems.py:843-844`
- Trigger: Trust-region method (`solve_method="trust_region"`) on problems where the linearized model alternates between under- and over-estimating the objective.
- Workaround: Time limit / `trust_region_iteration_limit` scenario parameter caps runtime but does not guarantee a good solution. Trust-region carries a runtime warning at `mesmo/problems.py:525` acknowledging it is experimental.

**Ambiguous ZeroDivisionError fallback in trust-region sigma:**
- Symptoms: When `(objective_power_flows_iter[-1] - objective_linear_model) == 0`, fallback sets `sigma = 0` with explicit doubt from author: "TODO: does this case really exist? should it evaluate to zero or 1?" (`mesmo/problems.py:848`).
- Files: `mesmo/problems.py:838-854`
- Trigger: Any trust-region iteration where candidate and previous objective are exactly equal.
- Workaround: None in-code. Adopt trust-region termination criterion from reference [2] of the docstring (Giacomoni & Wollenberg 2010) and encode expected behavior.

**Pump power sensitivity acknowledged wrong:**
- Symptoms: Comments state "Revise pump power sensitivity equation" and "Fix pump power sensitivity."
- Files: `mesmo/thermal_grid_models.py:741`, `mesmo/thermal_grid_models.py:974`
- Trigger: Any linear thermal grid model sensitivity calculation used in optimization.
- Workaround: None. Validation of thermal DLMP prices depends on correct sensitivity.

**CHP cost defined twice:**
- Symptoms: Source flags "Related: Cost for CHP defined twice" at `mesmo/der_models.py:1863` — marginal cost contribution potentially double-counted for CHP DERs.
- Files: `mesmo/der_models.py:1862-1864`
- Trigger: Optimal operation problem including a CHP DER.
- Workaround: Audit CHP objective contribution; verify the active + thermal cost terms are not both applied.

**Silent NaN-fill in DER timeseries:**
- Symptoms: Missing DER timeseries values silently replaced with 0.0 after resample/interpolate, no warning (`mesmo/data_interface.py:605-606`).
- Files: `mesmo/data_interface.py:600-607`
- Trigger: Any DER timeseries definition with gaps after resample to scenario `timestep_interval`.
- Workaround: Downstream code at `mesmo/data_interface.py:622-629` does warn for the non-accumulative branch — extend the same warning to the accumulative branch.

**OpenDSS global circuit state is not reset between models:**
- Symptoms: "TODO: Add reset method to ensure correct circuit model is set in OpenDSS when handling multiple models." (`mesmo/electric_grid_models.py:952`). `OpenDSSDirect.py` is a singleton; constructing a second `ElectricGridModelOpenDSS` while the first is still in use will silently overwrite circuit state.
- Files: `mesmo/electric_grid_models.py:892-1140` (the whole class), `opendss_command_string = "clear"` at `mesmo/electric_grid_models.py:964` is the only reset.
- Trigger: Running multiple scenarios in parallel or sequentially within one Python process without calling `clear` between them (any parameter sweep script).
- Workaround: Always run in separate processes (matches `multiprocessing.run_parallel = True` default) or manually issue `opendssdirect.Command("clear")` before building a new model.

**Example `test_examples.py` imports may leak module state across tests:**
- Symptoms: `sys.modules[example_file.stem] = module` is set but never removed. If two example scripts share a module name (e.g. both defined as `__main__` via different paths), later imports may shadow earlier ones.
- Files: `tests/test_examples.py:34-37`
- Trigger: Running full test suite; publication scripts already excluded due to "HiGHS solver errors" per `tests/test_examples.py:18`.
- Workaround: Delete from `sys.modules` and pop parent directory from `sys.path` in a `finally` block.

## Security Considerations

**`pickle.load()` on user-provided paths (arbitrary code execution risk):**
- Risk: `mesmo.utils.ResultsBase.load(results_path)` calls `pickle.load` on any `.pkl` file under the supplied `results_path`. A malicious `.pkl` file will execute arbitrary Python code during deserialization.
- Files: `mesmo/utils.py:12,132,151-152`
- Current mitigation: None. Only the file extension is checked; there is no signature verification or integrity check.
- Recommendations:
  - Document loudly in `ResultsBase.load()` that only trusted result directories should be loaded.
  - Replace `pickle` with `joblib` + HMAC signature, or migrate non-DataFrame results to JSON/Parquet where possible.
  - Add a `load(..., allow_pickle: bool = False)` kwarg so users opt in.

**`subprocess.Popen(..., shell=True)` with config-derived paths:**
- Risk: `solve_highs()` invokes HiGHS via shell with `command` built from `mesmo.config.config['paths']['highs_solver']` and temp paths. `shell=True` expands the full command string through the shell; a malicious `config.yml` or a results path containing shell metacharacters could inject commands. Similarly, `mesmo.utils.launch()` uses `shell=True` for `open`/`xdg-open` on a user-supplied `pathlib.Path`.
- Files: `mesmo/solutions.py:1182-1190`, `mesmo/utils.py:532-534`
- Current mitigation: Paths typically come from generated results folders, not untrusted user input, but nothing enforces this.
- Recommendations:
  - Drop `shell=True`; pass the command as a list (`subprocess.Popen([cfg, "--model_file", str(p), ...])`). Same fix for `launch()`.
  - If retaining `shell=True` is required for Windows compatibility, use `shlex.quote` for every interpolated path.

**`tarfile.extractall` without member filtering (path traversal, CVE-2007-4559):**
- Risk: `development_setup.py` downloads the HiGHS tarball and calls `file.extractall(base_path / "highs")` without `filter=` argument. A malicious tarball could write outside the target directory (`../`) or overwrite files.
- Files: `development_setup.py:75-76`
- Current mitigation: Tarball is fetched over HTTPS from a pinned GitHub release URL. Protection depends entirely on the integrity of the JuliaBinaryWrappers release.
- Recommendations:
  - Python 3.12+: pass `filter='data'` to `extractall`. The project requires Python 3.10, so conditionally apply for 3.12+ and fall back to a manual member validator on older interpreters.
  - Verify the tarball SHA256 against a pinned digest before extraction.

**Dynamic example script execution via `importlib.util.spec_from_file_location`:**
- Risk: `tests/test_examples.py` loads every `.py` file under `examples/` and executes its `main()`. If a user drops an arbitrary script into `examples/`, it runs under the test runner with full filesystem access.
- Files: `tests/test_examples.py:14-39`
- Current mitigation: Only the maintainers' CI runs these tests.
- Recommendations: Allowlist example names in `tests/test_examples.py`, or move scripts under a fixed prefix (e.g. `examples/tested/`).

**Local `config.yml` written unconditionally on first import:**
- Risk: `mesmo.config.get_config()` creates `./config.yml` in the repo root on first import if missing. For a globally installed `mesmo` this writes into the install directory which may be privileged.
- Files: `mesmo/config.py:22-33`
- Current mitigation: None.
- Recommendations: Write to a user-scoped directory (e.g. `platformdirs.user_config_dir("mesmo")`) or skip file creation when the package is installed into a read-only location.

**No `.env` / secrets file committed or loaded** — dynaconf is used only for YAML configuration; no API keys or credentials are read. Low ongoing secret-leak risk, but treat as a preventive pattern not a guarantee.

## Performance Bottlenecks

**Full sparse-matrix inversion via `scipy.sparse.linalg.inv`:**
- Problem: `mesmo/electric_grid_models.py:647-649` computes an explicit inverse of the no-source node admittance matrix. Explicit inversion is rarely the right operation for sparse systems — it densifies and scales O(n³).
- Files: `mesmo/electric_grid_models.py:647`
- Cause: Downstream linear model code (e.g. `mesmo/electric_grid_models.py:2231,2358`) multiplies by this inverse repeatedly, so the author pre-computed it.
- Improvement path: Cache an LU factorization (`scipy.sparse.linalg.splu`) and reuse `.solve()` instead of materializing the inverse. For networks > ~1000 nodes this is a substantial speedup and avoids fill-in blowup.

**Ray is eagerly initialized on first parallel task:**
- Problem: `mesmo/utils.py:194` calls `ray.init(...)` inside `starmap` on first use, which pays a multi-second startup cost even when only a handful of function calls would run. `chunk_count` in `chunk_dict` / `chunk_list` defaults to `os.cpu_count()` (`mesmo/utils.py:212,223`), so tiny inputs still spawn all cores.
- Files: `mesmo/utils.py:181-209,212-229`
- Cause: No heuristic for "small workload → run serial".
- Improvement path: Skip `ray.init` when `len(argument_sequence)` is below a threshold (e.g. 4) and always fall back to sequential execution. Also cap `chunk_count` at `len(input)`.

**Dense `np.set_printoptions(threshold=np.inf, linewidth=np.inf)`:**
- Problem: `mesmo/config.py:127` globally configures numpy to print arrays in full. Any accidental `print(array)` or error-message interpolation on a 10k-element vector will hang or produce enormous logs.
- Files: `mesmo/config.py:127`
- Cause: Intentional — makes results reproducible in logs.
- Improvement path: Scope print options via `np.printoptions` context manager around the specific result-saving paths, not globally.

**Pandas `set_option("display.width", int(9e9))` and unlimited rows:**
- Problem: Same category as above — any DataFrame printed to logs at error time balloons.
- Files: `mesmo/config.py:131-133`
- Cause: Intentional full-print for results inspection.
- Improvement path: Bounded context manager at the specific print sites.

**`starmap` serializes every argument through Ray even for pure-Python loops:**
- Problem: `ray_starmap` creates a new `ray.remote(lambda ...)` per argument tuple (`mesmo/utils.py:268-270`). Lambda capture + serialization per call dominates cost for microtasks.
- Files: `mesmo/utils.py:261-270`
- Cause: Design prefers ray over multiprocessing.
- Improvement path: Materialize `ray.remote(function_handle)` once and call `.remote(*args)` per tuple; avoid the lambda wrapper.

## Fragile Areas

**OpenDSS global singleton:**
- Files: `mesmo/electric_grid_models.py:892-1140` (entire `ElectricGridModelOpenDSS` class)
- Why fragile: `opendssdirect` holds one global circuit; two models cannot coexist in one process. Parallel scenarios *must* run in separate processes (which the Ray default provides, but this is not documented alongside the class).
- Safe modification: Never build two `ElectricGridModelOpenDSS` instances serially without an explicit `opendssdirect.Command("clear")` between them. Add a `__del__` or context-manager protocol.
- Test coverage: No test exercises two-model-in-one-process. Gap.

**Trust-region optimization:**
- Files: `mesmo/problems.py:504-921`
- Why fragile: Runtime warning on use (`mesmo/problems.py:524-528`), multiple in-source doubts about sigma behavior (`mesmo/problems.py:843,848,863`), and parameter names are documented only as inline literals (`delta_max`, `gamma`, `eta`, `tau`, `epsilon`, `trust_region_iteration_limit`, `infeasible_iteration_limit`).
- Safe modification: Do not ship optimizer changes without a validation scenario that checks convergence against an analytic answer (currently missing).
- Test coverage: `tests/test_problems.py` exists (39 lines) but is minimal; no dedicated trust-region convergence test detected.

**Dynaconf implicit config merge:**
- Files: `mesmo/config.py:36-42`
- Why fragile: `merge_enabled=True` silently merges `./config.yml` onto defaults. A malformed user config key is accepted and only surfaces as a downstream `KeyError` deep inside a model constructor.
- Safe modification: Validate against a pydantic or dataclass schema at `get_config()` time. Fail fast with a useful message.
- Test coverage: No config-validation tests.

**Type-checked attribute setting via `typing.get_type_hints`:**
- Files: `mesmo/utils.py:53-64` (`ObjectBase.__setattr__`)
- Why fragile: Every attribute assignment runs `typing.get_type_hints(type(self))` which imports and introspects the class — slow, and will emit false warnings during partially-initialized construction of subclasses with forward references.
- Safe modification: Cache the set of valid names on the class (e.g. `cls._valid_attributes = frozenset(...)`) once, not per `__setattr__` call.
- Test coverage: None for warning-emission behavior.

**Backwards-compatibility-hack `logger.warning` in placeholder classes:**
- Files: `mesmo/electric_grid_models.py:877-889`, `mesmo/utils.py:570-584`
- Why fragile: Using `logger.warning` instead of `DeprecationWarning` makes the message impossible to suppress via `warnings.filterwarnings` and invisible to `pytest --errors-on-warning` tooling.
- Safe modification: Replace with `warnings.warn(..., DeprecationWarning, stacklevel=2)`.

**In-process file-based `temp_path` for HiGHS:**
- Files: `mesmo/solutions.py:1147-1212`
- Why fragile: `get_results_path("temp")` creates a new timestamped directory under `results/` for every solve. Concurrent solves are safe, but (a) results folder accumulates `temp_...` directories indefinitely, (b) `cleanup()` at `mesmo/utils.py:587` is the only cleanup and requires manual invocation, (c) `problem.mps` + `solution.txt` parsing breaks if HiGHS output format changes.
- Safe modification: Use `tempfile.TemporaryDirectory()` instead of a subdirectory under `results/`. Move temp detritus out of the user-facing results tree.

## Scaling Limits

**Node admittance inversion:**
- Current capacity: Tested scenarios are small-to-medium distribution networks (e.g. `singapore_tanjongpagar`). No documented limit.
- Limit: Explicit `scipy.sparse.linalg.inv` on `node_admittance_matrix_no_source` will blow up memory for networks with thousands of nodes (see Performance Bottlenecks).
- Scaling path: Switch to LU factorization + solve (documented above).

**Ray default CPU share:**
- Current capacity: `mesmo/utils.py:194` uses `cpu_share * os.cpu_count()` with `cpu_share` from `mesmo.config.config["multiprocessing"]["cpu_share"]`.
- Limit: Hosts with > 128 cores: each Ray worker replicates the global SQLite connection and config, memory grows linearly in worker count.
- Scaling path: Cap workers by memory headroom, not by CPU count alone.

**SQLite concurrent access:**
- Current capacity: `connect_database()` comments note "Set large timeout to allow concurrent access during parallel processing" (`mesmo/data_interface.py:129`).
- Limit: SQLite locks the entire database on writes; Ray parallel `import_csv_file` calls that write to the same DB will serialize under the hood.
- Scaling path: Use a real DBMS (Postgres, DuckDB) for large-scenario datasets, or switch to a write-once-read-many Parquet layout.

## Dependencies at Risk

**`scipy<1.11` pin for CVXPY compatibility:**
- Risk: Hard upper-bound in `pyproject.toml:38` locks the project to SciPy < 1.11 (released mid-2023). Cuts off security patches and performance improvements in the 1.11/1.12/1.13/1.14+ line (nearly 3 years of releases as of 2026-04-20).
- Impact: Cannot benefit from upstream SciPy fixes; surface for transitive CVE advisories grows over time; may block coexistence with other modern scientific-Python projects in the same environment.
- Migration plan: Track CVXPY's SciPy compatibility. As of CVXPY 1.4+ the constraint was relaxed; bump minimum `cvxpy` and remove the upper-bound pin.

**`gurobipy` hard dependency:**
- Risk: `pyproject.toml:24` lists `gurobipy` as a mandatory dependency. `gurobipy` requires a commercial license for non-trivial problems; `mesmo/solutions.py:1154` notes HiGHS solves still go through Gurobi to export the MPS file.
- Impact: Users without a Gurobi license fall back to the unlicensed trial solver which silently truncates at 2000 variables.
- Migration plan: Make `gurobipy` an optional extra; add an MPS writer that does not require Gurobi (e.g. via `highspy` directly or `pyomo`). HiGHS has a native Python interface (`highspy`) that would also eliminate the `subprocess` + `shell=True` call path.

**`opencv-python-headless` as a hard dep:**
- Risk: `pyproject.toml:31` lists OpenCV as mandatory but OpenCV is only used by plotting utilities (I did not find any `cv2` imports in `mesmo/` source — likely a transitive `cobmo` or `plotly-kaleido` concern).
- Impact: Heavy wheel install for users who do not need image rendering.
- Migration plan: Verify actual usage; move to the `plots` extras group if optional.

**`cobmo` not on PyPI:**
- Risk: `pyproject.toml:21` comment — must be manually installed from GitHub (`https://github.com/mesmo-dev/cobmo`). Not reproducible without `development_setup.py`.
- Impact: `pip install mesmo` will fail for anyone who does not know about the submodule workflow.
- Migration plan: Publish `cobmo` to PyPI or use a `git+https://` direct URL dependency.

**Pinned HiGHS 1.2.2 binary:**
- Risk: `development_setup.py:60` downloads HiGHS 1.2.2 (released Dec 2022). Current HiGHS is 1.9+ with many solver improvements and fixes.
- Impact: Users get older solver; any fixed correctness issue in post-1.2.2 HiGHS is not available.
- Migration plan: Bump to latest HiGHS binary, or adopt `highspy` as the runtime solver interface.

**Ray `[default]` extras for trivial parallelism:**
- Risk: `pyproject.toml:36` pulls in Ray with default extras. Ray is a heavyweight distributed-computing framework for what is mostly CPU-parallel starmap.
- Impact: Large install surface, extra CVE exposure, longer cold-start.
- Migration plan: Evaluate replacing with `multiprocessing.Pool` or `concurrent.futures.ProcessPoolExecutor` for non-distributed use cases.

**No ARM64 HiGHS binaries:**
- Risk: `development_setup.py:61-66` hard-codes `x86_64` architecture strings. Apple-Silicon (`darwin-arm64`) and ARM-Linux hosts will install the wrong binary (or fail extraction).
- Impact: Blocks use on M1/M2/M3/M4 Macs without Rosetta, and on ARM-Linux clusters.
- Migration plan: Detect `platform.machine()` and select the appropriate `aarch64-*` / `arm64-*` HiGHS build.

## Missing Critical Features

**No structured deprecation mechanism:**
- Problem: No use of `warnings.warn` / `DeprecationWarning` / `FutureWarning` anywhere in `mesmo/`. Deprecations are communicated via `logger.warning` only.
- Blocks: Library consumers cannot suppress-per-version, cannot treat-as-error in their own test suites, cannot detect upcoming removals at import time.

**No input validation layer for `config.yml`:**
- Problem: Dynaconf merges user config without schema validation (`mesmo/config.py:36-42`).
- Blocks: Mistyped keys silently shadow defaults; failure mode is an opaque `KeyError` deep in a solve.

**No `__version__` exposed from package:**
- Problem: `mesmo/__init__.py` is 12 lines (see `wc -l`). Version is in `pyproject.toml` but not surfaced as `mesmo.__version__`.
- Blocks: User bug reports cannot include version without shelling out to `pip show`.

**No typed public API boundary:**
- Problem: Modules re-export implementation classes without an explicit `__all__`. Everything is "public" by default.
- Blocks: Backwards-compatibility guarantees unclear; refactors risk breaking downstream users silently.

**No timeouts on `subprocess.Popen` calls:**
- Problem: `mesmo/solutions.py:1182-1194` (HiGHS solve) streams `process.stdout` until EOF without wall-clock timeout. Same for `launch()` at `mesmo/utils.py:532-534`.
- Blocks: If HiGHS hangs, the Python process hangs. `time_limit` option is passed in the options file but is not enforced process-side.

**Pre-commit / formatter enforcement missing:**
- Problem: `pyproject.toml` configures `pylint` with several rules disabled (`function-redefined`, `too-many-lines`, etc.) but no `black`, `ruff`, or `pre-commit` config found.
- Blocks: Style drift; PR reviews spent on formatting.

## Test Coverage Gaps

**Trust-region optimizer has no dedicated test:**
- What's not tested: Convergence, oscillation handling, parameter sensitivity for `solve_trust_region` (`mesmo/problems.py:504-921`).
- Files: No test file targets `solve_trust_region` specifically; `tests/test_problems.py` (39 lines) only smoke-tests top-level solve.
- Risk: Silent regressions in a solver flagged experimental.
- Priority: High.

**Example publication scripts are explicitly excluded from CI:**
- What's not tested: Everything under `examples/publications/`.
- Files: `tests/test_examples.py:18-19` — comment "Excluded publication scripts from tests due to HiGHS solver errors".
- Risk: Publication results may silently break with library changes.
- Priority: High — the publications are the library's correctness evidence.

**OpenDSS electric grid model has 45 lines of tests:**
- What's not tested: Multi-model scenarios in one process, tap-changer behavior (hard-coded to 1.0 at `mesmo/electric_grid_models.py:461,464`), delta-connected DERs (TODO at `mesmo/electric_grid_models.py:573`).
- Files: `tests/test_electric_grid_models.py` (45 lines)
- Risk: Model correctness regressions go undetected.
- Priority: High.

**`test_template.py` contains a failing-by-design test:**
- What's not tested: Unclear purpose — `test_not_equal` asserts `2 + 1 != 4`, which holds, but `tests/test_template.py` advertises itself as a template.
- Files: `tests/test_template.py`
- Risk: Confuses new contributors about whether this file should be copied.
- Priority: Low (cosmetic) — delete or relocate to a template directory.

**No security / fuzz coverage for `ResultsBase.load()`:**
- What's not tested: `pickle.load` happy path only. No malicious-pickle guard tested.
- Files: `mesmo/utils.py:134-158`, no test file exercises it.
- Risk: RCE via crafted `.pkl`.
- Priority: Medium-High (depends on threat model — if only trusted result dirs, lower priority but still document).

**No test for `mesmo/utils.py::ObjectBase.__setattr__` warning behavior:**
- What's not tested: The warning-on-undefined-attribute contract advertised in the docstring.
- Files: `mesmo/utils.py:53-64`
- Risk: Silent regression of the invariant that keeps results objects consistent.
- Priority: Medium.

**No test for dynaconf config merging:**
- What's not tested: Behavior when `config.yml` is malformed, partial, or missing.
- Files: `mesmo/config.py:15-51`
- Risk: Config regressions surface only in downstream users' environments.
- Priority: Medium.

**No coverage for `launch()` or `cleanup()` utilities:**
- What's not tested: `mesmo/utils.py:523-534` (`launch`), `mesmo/utils.py:587-595` (`cleanup` — deletes results directory contents).
- Risk: `cleanup()` recursively deletes the `results/` tree; a bug could nuke user data.
- Priority: Medium.

**Total test LOC: 453 lines against 14,137 lines of source (~3%):**
- What's not tested: Broad coverage gap across all modules except the thin API smoke tests.
- Risk: Refactors rely heavily on downstream example scripts passing.
- Priority: High — add unit tests for pure functions in `utils.py`, numeric validators in `electric_grid_models.py`, and schema parsers in `data_interface.py`.

---

*Concerns audit: 2026-04-20*
