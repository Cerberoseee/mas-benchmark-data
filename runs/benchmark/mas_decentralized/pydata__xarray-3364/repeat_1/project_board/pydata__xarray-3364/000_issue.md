Title: Ignore missing variables when concatenating Datasets

Summary:
Several users reported that xarray.concat currently requires all Datasets to have the same variables. If some datasets are missing variables, users must either create dummy variables (filled with NaN) or drop mismatched variables before concatenation. pandas.concat is more permissive and does an outer join of columns; xarray.concat should offer the same behavior (include missing variables filled with NaN) or an option to do so.

Failing tests:
- xarray/tests/test_combine.py::TestAutoCombineOldAPI::test_auto_combine_with_new_variables
- xarray/tests/test_concat.py::TestConcatDataset::test_concat_merge_variables_present_in_some_datasets

Goal:
Make xarray.concat (and related auto-combine) tolerant of datasets with different variable sets by including variables present in some datasets and filling missing values with NaN. Keep change surface minimal and targeted to concat/auto-combine codepaths.

Constraints & notes:
- Do not redesign API. Prefer a minimal behavioral change consistent with tests.
- Tests in harness already expect this behavior; implement to satisfy them.
- Typical flow: Engineer -> CodeReviewer -> QA. Ensure a non-empty patch is committed before declaring completion.

Next steps: see tickets below.
