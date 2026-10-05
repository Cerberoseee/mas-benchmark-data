Repository: mwaskom/seaborn
Issue: pairplot raises KeyError with MultiIndex DataFrame

Goal: Fix pairplot to accept DataFrames with MultiIndex columns without raising KeyError.

Work flow:
- Triage the failing test tests/test_axisgrid.py::TestPairGrid::test_pairplot_column_multiindex
- Create focused tickets for diagnosis, fix, review, and QA
- Route to Engineer, then CodeReviewer, then QA, then finalize

Notes:
- Prefer minimal changes to axisgrid.PairGrid / pairplot logic
- Tests: harness already applied a failing test patch; implement fix in code
