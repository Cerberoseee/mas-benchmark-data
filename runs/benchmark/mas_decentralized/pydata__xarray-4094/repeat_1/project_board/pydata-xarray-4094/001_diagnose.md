Diagnose to_unstacked_dataset failure

Objective: Find the source of MergeError when calling to_unstacked_dataset on a stacked DataArray created from a Dataset where the variables are single-dimension.

Tasks:
- Search for to_unstacked_dataset implementation in repository.
- Reproduce failing test locally (run the provided MCVE and the failing unit test xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset)
- Inspect how coords and data_vars are combined in unstacking path. Look for places that merge/concat datasets or variables and perform compatibility checks.
- Hypothesis: when variables after stacking have no remaining non-stacked dimensions (i.e., only the stacked dimension), unstacking may attempt to merge the stacked coordinate (named 'y' in example) across variables, causing MergeError because each variable carries its own coordinate with same name but different values.
- Identify minimal change to avoid conflicts: either drop duplicated variable/coord before merge or use compat='override' for merging in this specific path.

Deliverable: patch proposal and pointer to exact function and lines to change.

Assignee: Engineer
Priority: high
Estimated time: 2-4h