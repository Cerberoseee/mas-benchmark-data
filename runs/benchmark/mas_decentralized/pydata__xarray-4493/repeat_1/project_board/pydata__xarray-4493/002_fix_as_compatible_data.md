Title: Fix as_compatible_data to preserve DataArray laziness

Goal:
Modify xarray.core.variable.as_compatible_data to treat DataArray objects by returning the underlying .data attribute instead of .values, so that dask-backed DataArrays remain lazy when used in dataset constructor/update tuple form.

Scope:
- Edit xarray/core/variable.py only.
- Add an isinstance check: if isinstance(data, (DataArray, Variable)): return data.data

Implementation notes for Engineer:
- Import DataArray at top-level of the module or use a local import to avoid circular imports.
- Preserve behavior for Variable as already implemented.
- Add/update unit tests: ensure TestAsCompatibleData::test_unchanged_types and test_full_like_dask retain expected behavior for dask arrays.
- Keep the change minimal and add an explanatory comment.

Deliverables:
- One commit implementing the change.
- Run pytest for xarray/tests/test_variable.py::TestAsCompatibleData::test_unchanged_types and the failing test(s).
