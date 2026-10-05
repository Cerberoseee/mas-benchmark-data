Ticket: QA-0001
Title: QA: Validate QDP parsing for mixed-case commands

Description:
Run the qdp test suite and additional manual tests to confirm lower-case and mixed-case QDP commands are accepted.

Acceptance criteria:
- All qdp-related tests pass (including astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]).
- Manual test: read a file containing "read serr 1 2" without errors and confirm errors parsed into Table.

QA Steps:
1. Run pytest for qdp tests.
2. If failures occur, include failing_ids and details in QA_VERDICT.

When verified true, include QA_VERDICT block in the report.
