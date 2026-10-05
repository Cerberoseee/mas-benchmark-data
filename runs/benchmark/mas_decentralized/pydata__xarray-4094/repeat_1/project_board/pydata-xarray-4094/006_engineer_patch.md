Engineer patch summary

Files changed:
- xarray/core/dataarray.py

Patch intent:
- When converting a stacked DataArray back to a Dataset via to_unstacked_dataset, for variables that are created by selecting a level along the stacked variable_dim and squeezing, drop the stacked coordinate named by `dim` from the per-variable DataArray before assembling into the final Dataset. This avoids MergeError caused by conflicting scalar coordinates with the same name on the individual variables.

Commit message:
fix(to_unstacked_dataset): drop stacked coordinate when unstacking single-dim variables (GH4049 regression)

Test results (selected):
- Initially failing test xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset passed after patch.

Notes:
- read_patch_diff confirmed the patch is present.
- Next: transfer to CodeReviewer for review and then QA.