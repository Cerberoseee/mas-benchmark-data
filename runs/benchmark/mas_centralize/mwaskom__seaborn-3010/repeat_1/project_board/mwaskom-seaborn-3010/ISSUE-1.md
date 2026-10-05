Title: PolyFit not robust to missing data

Repository: mwaskom/seaborn
Base commit: 0f5a013e2cf43562deec3b879458e59a73853813

Problem:
PolyFit raises an exception when input data contains missing values (NaN/None). The failing example:

so.Plot([1, 2, 3, None, 4], [1, 2, 3, 4, 5]).add(so.Line(), so.PolyFit())

Traceback indicates numpy.polyfit is called with arrays containing missing values, leading to LinAlgError (SVD did not converge) rather than gracefully handling missing data.

Failing tests:
- tests/_stats/test_regression.py::TestPolyFit::test_missing_data

Goal:
Make PolyFit robust to missing data by dropping missing observations before calling numpy.polyfit, without changing behavior for other cases. Keep change minimal and include tests.

Constraints:
- Don't modify tests. Harness already applied gold test patch.
- Prefer minimal implementation change.

Plan (high-level):
1. Investigate current PolyFit implementation to find where x, y arrays are prepared before polyfit.
2. Add logic to drop rows where x or y are NA (np.isnan / pandas.isna) prior to calling np.polyfit. Ensure this works with pandas Series and numpy arrays and preserves dtype.
3. Add unit tests if needed (harness may have provided). Run tests.
4. Iterate with QA.

Next steps:
- Create focused tickets and assign to Engineer/CodeReviewer/QA as needed.
- Hand off to Engineer to implement the fix.
