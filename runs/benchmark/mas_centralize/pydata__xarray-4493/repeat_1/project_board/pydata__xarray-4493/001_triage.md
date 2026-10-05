Triage notes for pydata/xarray issue #4493

Summary:
- Bug: Dataset.update (and Dataset constructor if using (dims, data) tuples) evaluates chunked dask DataArray because as_compatible_data doesn't handle DataArray and falls back to DataArray.values.
- Failing test: xarray/tests/test_variable.py::TestVariable::test_as_variable

Root cause hypothesis:
- In xarray/core/variable.py as_compatible_data checks for supported data types but doesn't include DataArray/Variable; when a DataArray is passed it ends up calling .values which forces computation of dask-backed arrays.
- Proposed minimal fix: modify as_compatible_data to handle DataArray and Variable by returning data.data (the underlying array object) rather than .values.

Files likely affected:
- xarray/core/variable.py

Plan:
- Create a small code change in as_compatible_data to detect DataArray/Variable and return .data.
- Add/update tests if necessary: there is already a failing test TestVariable::test_as_variable; ensure it passes.
- Keep changes small to avoid side effects.

Next steps:
- Delegate implementation to Engineer ticket 002_implement
- After patch, run tests: at minimum run failing test and dask tests

Notes:
- The issue originated in upstream discussion; change aligns with suggested fix from contributor.
- Be careful: as_compatible_data is used in many paths; return types must remain consistent (e.g., numpy arrays, dask arrays, pandas objects, etc.).

