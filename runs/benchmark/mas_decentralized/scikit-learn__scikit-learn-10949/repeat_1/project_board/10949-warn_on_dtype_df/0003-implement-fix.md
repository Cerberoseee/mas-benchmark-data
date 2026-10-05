Implementation task: apply minimal change to warn_on_dtype behavior for pandas DataFrame

Goal:
- Ensure check_array emits DataConversionWarning when warn_on_dtype=True and input is a pandas DataFrame that will be converted from object dtype to float64.

Constraints:
- Minimal surface change; prefer to add a detection branch for pandas DataFrame to reuse existing numpy path.
- Do not modify tests.

Acceptance criteria:
- Tests pass for test_check_dataframe_warns_on_dtype and no regressions.

Assignee: Engineer (Alice)
