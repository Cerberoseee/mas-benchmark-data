Status: Fixed
Engineer: Charlie
Commit: ad6cfe30

Summary:
- Drop missing x/y values before fitting in PolyFit._fit_predict to avoid Linear Algebra errors when data contain NaNs.
- Minimal change: seaborn/_stats/regression.py

Validation:
- Ran targeted tests: tests/_stats/test_regression.py::TestPolyFit::test_missing_data, test_no_grouper, test_one_grouper — all passed locally.

Next steps:
- Request code review (see TICKET-2-code-review.md).
- QA to verify visual outputs (TICKET-3-qa.md).
