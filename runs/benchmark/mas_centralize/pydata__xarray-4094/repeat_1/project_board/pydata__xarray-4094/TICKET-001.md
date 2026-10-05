TICKET-001: Investigate failing test

Description:
- Run the failing test xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset
- Reproduce the error locally, inspect stack/unstack code path, and find where MergeError originates when variables have only a single dimension.

Update (Engineer done):
- Engineer reproduced the failure and implemented a minimal fix in xarray/core/dataarray.py:
  - After selecting and squeezing each variable from the stacked DataArray, if the stacked dimension name appears as a scalar coordinate on the resulting DataArray, drop it to avoid conflicting scalar coords when combining into a Dataset.
- Patch: fix: drop stacked dim coord when unstacking DataArray to Dataset (GH4049 regression)
- Tests: failing test now passes locally.

Acceptance criteria:
- Reproduce failure and identify the minimal code location and root cause.

Assignee: Engineer