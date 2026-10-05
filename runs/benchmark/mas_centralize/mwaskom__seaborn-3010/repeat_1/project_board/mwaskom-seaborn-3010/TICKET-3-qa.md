TICKET-3: QA validation for PolyFit missing-data fix

Description:
Run the test suite or the targeted regression tests to confirm the PolyFit missing-data fix resolves the failing test(s).

Test targets:
- tests/_stats/test_regression.py::TestPolyFit::test_missing_data (must pass)
- tests/_stats/test_regression.py::TestPolyFit::test_no_grouper
- tests/_stats/test_regression.py::TestPolyFit::test_one_grouper

Provide QA_VERDICT block with verified: true/false, failing_ids and notes if false.

Assignee: QA
