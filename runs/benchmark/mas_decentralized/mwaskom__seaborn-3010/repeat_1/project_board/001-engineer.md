Engineer ticket: Implement missing-data handling in PolyFit

Files to modify:
- seaborn/_stats/regression.py

Requirements:
- In PolyFit._fit_predict, before calling np.polyfit, drop rows where x or y are NaN/None.
- If after dropping, there are fewer than (order + 1) points (np.polyfit requires at least order+1), return empty xx, yy lists instead of calling np.polyfit.
- Maintain existing behavior for non-missing data.

Acceptance criteria:
- Patch is non-empty and committed (read_patch_diff will show it).
- Tests pass locally (CI will be run by QA).

Hints:
- Use pandas.isna or np.isfinite to filter numeric arrays. Inputs to _fit_predict may be pandas Series or numpy arrays.
- Keep changes minimal and local to _fit_predict.
