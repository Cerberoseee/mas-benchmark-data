Project: pydata/xarray issue #4493 - DataSet.update causing dask DataArray to compute

Goal: Fix xarray.core.variable.as_compatible_data so that passing a DataArray (and Variable) preserves lazy dask-backed arrays instead of falling back to .values which triggers compute.

Constraints:
- Keep change minimal and narrowly scoped to xarray/core/variable.py
- Do not alter public APIs beyond preserving laziness
- Ensure existing dask-related tests still pass

Workflow:
1. Engineer: run failing test, implement minimal change, produce patch
2. CodeReviewer: review diff for correctness and scope
3. QA: run test suite subset and verify QA_VERDICT
4. ProjectManager (PM): confirm patch diff non-empty and QA verified true, then close

Tickets created below.