Title: Diagnose as_compatible_data handling of DataArray (bug triage)

Goal:
Confirm root cause: Dataset.update (and Dataset constructor using (dims, data) tuples) forces DataArray -> numpy conversion because xarray.core.variable.as_compatible_data falls back to .values for DataArray, triggering dask computation.

Steps for Engineer:
1. Reproduce the minimal example from the issue in a local test script and with pytest for the failing test xarray/tests/test_variable.py::TestVariable::test_as_variable. Use the repository commit at head of the workspace.
2. Add debugging/logging or interactive inspection to confirm that when passing a DataArray object into as_compatible_data it is not handled by the existing condition(s) and that the code reaches the fallback path that calls getattr(data, "values", data).
3. Locate xarray/core/variable.py::as_compatible_data and inspect the branch that handles Variable and numpy-like types. Confirm whether DataArray is intentionally excluded at that level.
4. Verify whether treating DataArray like Variable (i.e. returning data.data) preserves laziness for dask arrays in the dataset.update path.
5. Run a subset of dask-related tests (xarray/tests/test_dask.py::TestVariable::test_basics and a couple others) to check for regressions during experimentation.

Expected outcome:
- Confirmed single-line root cause: as_compatible_data should treat DataArray by returning .data instead of .values, avoiding computation. This will guide the fix implementation.

Notes:
- Keep changes minimal: the fix is probably a small isinstance check in as_compatible_data.
- If diagnostics find that other call sites expect a concrete ndarray for DataArray in this function, document them here.
