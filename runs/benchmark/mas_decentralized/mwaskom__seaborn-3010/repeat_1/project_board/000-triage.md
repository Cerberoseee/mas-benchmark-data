Title: PolyFit: handle missing data robustly

Issue: PolyFit (seaborn._stats.regression.PolyFit) raises a LinAlgError when inputs contain missing values (NaN/None). A failing test: tests/_stats/test_regression.py::TestPolyFit::test_missing_data

Goal: Fix PolyFit so it gracefully handles missing data by dropping NaN rows before fitting.

Scope: Minimal change to seaborn/_stats/regression.py to filter out missing x or y values in the _fit_predict method. Add no new public API or behavior changes except improved robustness.

Steps:
- Engineer: Implement filtering of NaN/None values in PolyFit._fit_predict before calling np.polyfit. Ensure that when all values are missing or too few points remain to fit the requested order, the method returns empty xx/yy arrays without raising.
- Add small unit adjustments if necessary.
- CodeReviewer: Review the patch for correctness and minimal surface.
- QA: Run the test suite and verify tests pass, especially the failing test.

Acceptance criteria:
- tests/_stats/test_regression.py::TestPolyFit::test_missing_data passes.
- Existing passing tests (no_grouper, one_grouper) continue to pass.
- Change limited to regression.py and minimal logic.

Notes:
- The test harness already applied the gold test patch.
- Ensure to use pandas.isna or numpy.isnan robustly for different input types.
- If the patch touches tests, revert; tests should be applied by harness only.
