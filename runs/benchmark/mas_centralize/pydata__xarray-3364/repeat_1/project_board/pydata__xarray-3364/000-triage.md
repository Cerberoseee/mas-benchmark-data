Issue: Ignore missing variables when concatenating datasets

Description:
- Users expect xarray.concat to handle datasets with mismatched variables by filling missing variables with NaN (i.e., outer join on variables), similar to pandas.concat behavior.

Failure:
- Two tests failing:
  - xarray/tests/test_combine.py::TestAutoCombineOldAPI::test_auto_combine_with_new_variables
  - xarray/tests/test_concat.py::TestConcatDataset::test_concat_merge_variables_present_in_some_datasets

Hypothesis:
- concat currently requires identical variable sets and raises or misbehaves when variables are missing in some datasets.
- Need to implement behavior to union variables across input datasets and fill with NA where missing, possibly controlled by a new kwarg or by default.

Plan:
1. Inspect concat implementation to find variable merging logic and join behavior.
2. Modify minimal code to allow union of variables across datasets during concat, filling missing variables with NaN or appropriate fill_value.
3. Run tests to see remaining failures and iterate.

Constraints:
- Make minimal changes, do not change public API unless necessary. Prefer an option like join='outer' already exists; if so, ensure variables missing are treated like coords/data_vars union.
- Ensure non-empty patch.

Next: Assign to Engineer to implement fix and run tests.
