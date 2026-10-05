Title: QA test plan for as_compatible_data fix

Objective:
Verify the fix preserves dask laziness when using Dataset.update or Dataset constructor with (dims, data) tuple and DataArray values, and that no dask-related tests regress.

Test cases for QA:
1. Reproduce user's minimal example showing ds.update converting chunked DataArray to numpy and verify fix preserves chunking.
2. Run xarray/tests/test_variable.py::TestAsCompatibleData::test_unchanged_types
3. Run failing test xarray/tests/test_variable.py::TestVariable::test_as_variable
4. Run a selected subset of dask tests: xarray/tests/test_dask.py::TestVariable::test_basics, test_copy, test_chunk, test_indexing
5. Run full test module xarray/tests/test_dask.py to be safe if time permits.

QA acceptance criteria:
- The updated DataArray remains a dask array (lazy) after ds.update with tuple form.
- The failing test(s) now pass.
- No regressions in the targeted dask tests.

Notes:
- If QA finds failures, include failing_ids and notes in QA_VERDICT block when handing back.
