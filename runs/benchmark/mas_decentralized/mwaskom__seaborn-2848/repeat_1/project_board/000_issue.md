Title: pairplot fails with hue_order not containing all hue values

Repo: mwaskom/seaborn
Issue: In seaborn 0.11.1, PairGrid/pairplot raises a TypeError when hue_order does not include all values present in the hue column. Previously, specifying a subset of hue levels would simply omit other points. This regression breaks code that relied on selecting a subset via hue_order.

Failing tests:
- tests/test_relational.py::TestScatterPlotter::test_hue_order

Symptoms:
- TypeError: ufunc 'isnan' not supported for the input types ... arises in seaborn/_core.py
- Occurs when PairGrid delegates hue to mapped axes functions but doesn't handle the case where grid-level hue is unset and.axes-level hue is set or when hue_order omits some hue values.

Requested fix:
- Restore previous behavior: allow hue_order to specify a subset of hue levels and plot only those, without raising.
- Minimal changes to PairGrid or handling in mapping to ensure missing hue values are filtered out early.

Notes:
- Workarounds exist (map with explicit hue series), but a fix in seaborn is preferred.
- Related discussion: need to ensure compatibility between PairGrid-level and axes-level hue semantics.
