Title: warn_on_dtype with DataFrame

Repo: scikit-learn/scikit-learn
Issue: warn_on_dtype has no effect when input is a pandas DataFrame

Summary:
check_array(..., warn_on_dtype=True) does not emit a DataConversionWarning when the input is a pandas DataFrame with dtype=object. The expected behavior is to warn when input dtype is object and conversion to float64 occurs.

Observed failure:
- Failing test: sklearn/utils/tests/test_validation.py::test_check_dataframe_warns_on_dtype
- Most related tests pass, including other dtype warning tests for ndarrays.

Likely root cause hypotheses:
- check_array may have special handling for pandas DataFrame, possibly using pandas' to_numpy() or values that produce array already cast to numeric without tracking original dtype; or warn_on_dtype check might be bypassed for DataFrame path.

Initial files to inspect:
- sklearn/utils/validation.py (where check_array is implemented)
- sklearn/utils/tests/test_validation.py (to see expected behavior and current test)

Next steps:
1. Read implementation in sklearn/utils/validation.py to find DataFrame-specific code path and warn_on_dtype handling.
2. Create focused tickets:
   - Investigate & implement fix in validation.py to ensure warn_on_dtype is honored for pandas DataFrame inputs with object dtype.
   - Add/adjust tests if necessary (but tests already exist and are failing).
   - Engineer implementation -> assign to Engineer.
   - Code review -> assign to CodeReviewer.
   - QA -> assign to QA.

I'll now create the tickets and route to the Engineer to implement the fix.
