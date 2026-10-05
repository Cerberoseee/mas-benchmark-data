CodeReview ticket: Review PolyFit missing-data patch

When the Engineer has implemented the change, run a code review focusing on:
- Correctness of NaN filtering across input types (pandas Series, numpy arrays, lists with None)
- Handling when too few points remain (should avoid np.polyfit and return empty predictions)
- Minimality of change and no edits to tests

Provide REVIEW_VERDICT with blocking_findings key set if there are issues.
