Status: Implemented

Engineer: Charlie

Summary:
- Fixed warn_on_dtype handling for pandas.DataFrame in sklearn/utils/validation.py. Now emits DataConversionWarning when DataFrame dtypes differ or are mixed. Minimal, localized change.

Files changed:
- sklearn/utils/validation.py: adjusted warn_on_dtype branch to inspect array_orig.dtypes for DataFrame and warn accordingly.

Testing performed:
- Ran targeted test: sklearn/utils/tests/test_validation.py::test_check_dataframe_warns_on_dtype -> PASSED
- Ran the listed Pass-to-pass tests from the ticket -> all PASSED

Commit: ENH: warn_on_dtype: handle pandas DataFrame dtypes and mixed dtypes in check_array (commit 2b998fa36)

Notes for reviewer/QA:
- The change only affects the warn_on_dtype path and only when the input has a pandas-like dtypes attribute.
- Behavior: if DataFrame has uniform dtype that differs from output dtype, we warn that were all converted; if mixed dtypes, we warn that mixed input dtypes were converted.

Next steps: please review the patch in sklearn/utils/validation.py and run broader test-suite if desired.