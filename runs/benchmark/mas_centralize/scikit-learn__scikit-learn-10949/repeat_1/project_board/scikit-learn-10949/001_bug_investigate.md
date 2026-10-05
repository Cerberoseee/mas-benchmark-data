Title: Investigate warn_on_dtype behavior for pandas DataFrame in check_array

Goal:
Find why check_array(..., warn_on_dtype=True) does not warn when passed a pandas DataFrame with dtype=object.

Tasks:
- Inspect sklearn/utils/validation.py for DataFrame handling and warn_on_dtype logic.
- Reproduce issue locally by running the failing test: sklearn/utils/tests/test_validation.py::test_check_dataframe_warns_on_dtype
- Determine whether DataFrame path uses pandas internals (e.g., DataFrame.values or DataFrame.to_numpy) and whether dtype information is lost or conversion happens earlier.
- Propose a minimal fix: ensure that when input is a DataFrame and warn_on_dtype=True, if the DataFrame's dtypes indicate object and conversion to float64 occurs, emit DataConversionWarning.

Acceptance criteria:
- Clear identification of the code region to change and a minimal change plan.
