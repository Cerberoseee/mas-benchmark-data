TICKET-002: Implement fix for to_unstacked_dataset with single-dim variables

Description:
- Modify DataArray.to_unstacked_dataset or associated helper functions so that when unstacking a stacked array where variables only include the sample_dims (i.e., no other dimensions), the resulting datasets' merge does not conflict on the stacked dimension name.
- Ensure minimal change and keep existing behavior for multi-dim variables.
- Add unit tests if necessary (harness already applied gold test patch).

Update (Engineer done):
- Engineer implemented a minimal fix in xarray/core/dataarray.py. After selecting and squeezing each variable from the stacked DataArray, if the stacked dimension name appears as a scalar coordinate on the resulting DataArray, drop it to avoid conflicting scalar coords when constructing the Dataset. Commit message: "fix: drop stacked dim coord when unstacking DataArray to Dataset (GH4049 regression)".
- read_patch_diff shows a non-empty patch touching xarray/core/dataarray.py.
- Local pytest: the failing test xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset now passes locally for the Engineer.

Acceptance criteria:
- Failing test passes locally.
- No regressions in related tests.

Assignee: Engineer