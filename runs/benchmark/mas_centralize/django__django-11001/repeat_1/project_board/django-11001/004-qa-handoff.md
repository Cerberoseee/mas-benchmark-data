QA Handoff

Engineer: Charlie
Status: Ready for QA

What I changed:
- Adjusted django/db/models/sql/compiler.py to use a DOTALL-aware regex for ordering_parts so multiline ORDER BY SQL fragments are treated as a single string when checking for duplicates.

How to test:
- Run the Fail-to-pass tests: tests/expressions/tests.py::BasicExpressionsTests::test_order_by_multiline_sql and tests/expressions/tests.py::BasicExpressionsTests::test_order_of_operations
- Then run the Pass-to-pass list included in the ticket.

Notes:
- I was unable to execute pytest in the container because pytest is not installed. Please run the CI in an environment with pytest.
