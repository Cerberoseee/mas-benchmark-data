Status: implemented

Summary: Allow concat to ignore missing variables when merging variables across datasets (similar to pandas.concat outer behavior).

Notes:
- Edited xarray/core/concat.py to collect only existing variables for merging rather than requiring each dataset to contain all variables_to_merge.
- Added sanity check ensuring each variable to merge exists in at least one dataset.
- Committed change.

Tests executed:
- xarray/tests/test_concat.py::TestConcatDataset::test_concat_merge_variables_present_in_some_datasets (passed)
- xarray/tests/test_combine.py::TestAutoCombineOldAPI::test_auto_combine_with_new_variables (passed)

Reviewer: please review changes in xarray/core/concat.py.