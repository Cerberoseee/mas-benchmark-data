Engineer tasks (implement fix):

Files likely involved:
- django/db/models/sql/compiler.py (SQLCompiler.get_order_by)
- expressions tests in tests/expressions (existing failing tests are in harness)

Implementation notes:
- Investigate ordering_parts regex and how sql variable is used. Consider using a one-line normalized SQL for the ordering_parts.search call (replace newlines with spaces) or make the regex DOTALL-aware so it matches full clause.
- Ensure not to break other uses; run pytest -q expressions.tests.BasicExpressionsTests::test_order_by_multiline_sql and test_order_of_operations.
- Commit changes; ensure patch.diff is produced for review.

Deliverables:
- Code changes in repository.
- Short commit message describing the fix.

When ready, transfer to CodeReviewer for review.
