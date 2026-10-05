QA tasks:

- Run impacted tests: expressions.tests.BasicExpressionsTests::test_order_by_multiline_sql and test_order_of_operations.
- Run nearby expressions test suite to ensure no regressions.
- Provide QA_VERDICT block with verified: true/false and failing_ids if any.

Notes:
- If failures indicate collection issues (not found/not collected/returncode=4), inform Engineer about test patch application issues.
