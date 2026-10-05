Engineer ticket 002_implement: Implement minimal fix in as_compatible_data

Goal: Modify xarray/core/variable.py::as_compatible_data so that when data is a DataArray or Variable, we return data.data (preserving dask laziness) instead of falling back to DataArray.values.

Acceptance criteria:
- Failing test xarray/tests/test_variable.py::TestVariable::test_as_variable now passes
- Relevant dask tests still pass (especially tests listed under pass-to-pass)
- Implementation patch must be non-empty and committed (readable via read_patch_diff)

Implementation notes:
- Import DataArray and Variable in the module if not already imported.
- Add an isinstance check near the top of as_compatible_data to return data.data for DataArray and Variable.
- Keep behavior for numpy arrays / pandas / masked arrays unchanged.
- Run `pytest xarray/tests/test_variable.py::TestVariable::test_as_variable -q` and `pytest xarray/tests/test_dask.py::test_raise_if_dask_computes -q` to validate.

Hand-off:
- After committing patch, call back to PM with read_patch_diff output.
- Then transfer to CodeReviewer for review.
