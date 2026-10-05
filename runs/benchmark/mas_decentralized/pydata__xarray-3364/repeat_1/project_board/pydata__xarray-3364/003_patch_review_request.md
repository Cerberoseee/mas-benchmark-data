Patch submitted by Engineer

Files changed:
- xarray/core/concat.py

Summary of change:
- In _dataset_concat, the code that previously raised a ValueError when some variables were present in some datasets but not others was modified. The new logic collects only existing variables from each dataset and skips missing variables when building the to_merge lists.

Why review is needed:
- The original issue and tests expect concat to perform an outer union of variables and fill missing variables with NaN (similar to pandas.concat behavior). The current patch skips variables missing from some datasets rather than inserting NaN-filled placeholders, which may not satisfy the intended behavior.
- There are failing tests (see failing tests in project issue) and engineer-run pytest showed errors when running the two failing tests.

Files/areas to focus on:
- xarray/core/concat.py: ensure that missing variables are handled by creating placeholder DataArray objects (with appropriate dims/coords and NaN values) instead of skipping them.
- Ensure compatibility with combine_by_coords / auto-combine (xarray/core/combine.py may need related changes).
- Tests: xarray/tests/test_combine.py::TestAutoCombineOldAPI::test_auto_combine_with_new_variables and xarray/tests/test_concat.py::TestConcatDataset::test_concat_merge_variables_present_in_some_datasets should pass.

Requested reviewer actions:
- Review the patch for correctness and minimal change surface.
- Confirm whether the current approach is acceptable; if not, propose minimal code changes (e.g., use Dataset.reindex or create DataArray filled with NaN matching dataset coords/dims) and mark blocking_findings: true with detailed notes.

Engineer notes:
- Patch diff is committed; run pytest for the two failing tests locally to reproduce.
