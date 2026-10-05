Review notes:
- Implemented minimal change in xarray/core/dataarray.py to drop stacked coord from per-variable DataArray before creating Dataset.
- Committed as: fix(to_unstacked_dataset): drop stacked coordinate when unstacking single-dim variables (GH4049 regression)
- Ran failing test and it passed.
- Ready for CodeReviewer and QA to run full test suite.