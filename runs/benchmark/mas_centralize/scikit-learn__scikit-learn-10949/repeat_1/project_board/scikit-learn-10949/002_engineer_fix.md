Status: Done

Engineer: Charlie
Date: 2026-05-15

Summary:
- Implemented minimal fix in sklearn/utils/validation.py to emit DataConversionWarning when warn_on_dtype=True for pandas.DataFrame.

Files changed:
- sklearn/utils/validation.py

Commit:
- FIX: warn_on_dtype for pandas DataFrame in check_array (gh-10948)

Tests:
- Ran failing test and relevant validation tests. All targeted tests passed.

Handoff: Ready for CodeReviewer and QA.
