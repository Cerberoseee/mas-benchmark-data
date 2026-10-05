Triage notes

Root cause hypothesis:
- PairGrid delegates hue to mapped functions if those functions accept a hue argument. When a mapped function receives a hue=series and hue_order that omits some categories, downstream code in _core or scatterplot tries to call isnan or otherwise operate on the hue values, which may be strings, leading to TypeError when mixing datatypes.
- More precisely, code expects a numeric mask (NaN) handling on the hue vector; if hue contains strings and hue_order omits some categories, the filtering step may produce boolean/masked arrays incompatible with np.isnan.

Impact:
- A single failing test in relational tests for hue_order. Likely affects PairGrid/pairplot with subset hue_order usage.

Plan:
1) Run tests locally to reproduce failure (harness already reports failing test).
2) Inspect code in seaborn/_core.py and seaborn/axisgrid.py (PairGrid) to find where hue and hue_order are processed and where filtering happens.
3) Implement minimal fix: when a hue_order is provided that is a subset of unique hue values, filter the data to include only rows with hue in hue_order before calling mapped functions. This can be done in PairGrid._attach_legend or in map methods where hue delegation occurs.
4) Add/update a targeted unit test if necessary (but harness already has failing test).
5) Run tests; iterate until passing.

Tickets to create:
- 010_fix_pairgrid_hue_subset.md: Implement the fix in PairGrid/map handling
- 020_review_fix.md: Code review ticket
- 030_qa_pairgrid_hue_subset.md: QA validation

Routing: Engineer implements 010, then transfer to CodeReviewer, then QA.
