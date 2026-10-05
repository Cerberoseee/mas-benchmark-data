T5 - QA verification

Objective:
Run relevant pytest tests and confirm QA_VERDICT.

Tests to run:
- tests/config/test_config.py::test_regex_error
- tests/config/test_config.py::test_csv_regex_error
- Optionally, run tests/config/test_config.py fully.

QA_VERDICT block should be provided with verified: true/false, failing_ids, and notes.

Assignee: QA