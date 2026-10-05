Implementation notes:
- Patched xarray/core/dataarray.py: to_unstacked_dataset now drops the stacked coordinate from each per-variable DataArray before creating the Dataset.
- Rationale: avoid MergeError when variables have only the stacked dimension and thus scalar stacked-coordinate values differ across variables.