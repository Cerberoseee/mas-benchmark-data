TICKET-005: Fix to_unstacked_dataset for single-dim variables

Status: In Progress (patched)

Notes:
- Identified regression where DataArray.to_unstacked_dataset included the stacked dimension as a scalar coordinate on per-variable DataArrays, causing MergeError when constructing Dataset.
- Applied minimal patch in xarray/core/dataarray.py to drop the stacked dimension coord on per-variable DataArrays before constructing Dataset.
- Ran targeted test xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset and it passed.

Please review patch and run full test suite as needed.