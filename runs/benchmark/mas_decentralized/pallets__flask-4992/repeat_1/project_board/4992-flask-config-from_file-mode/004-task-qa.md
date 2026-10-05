Title: QA: Run tests and verify fix

Description:
Run test suite (or targeted tests) and verify that tests/test_config.py::test_config_from_file_toml now passes and no regressions are introduced.

QA_VERIFICATION:
- verified: bool
- failing_ids: list[str]
- notes: str

Assign to: QA
