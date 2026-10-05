Issue: Improve default logging format to include module name (`%(name)s`) instead of just the base filename.

Repository: pytest-dev/pytest
Base commit: 2051e30b9b596e944524ccb787ed20f9f5be93e3

Failing tests (from harness):
- testing/logging/test_reporting.py::test_log_cli_enabled_disabled[True]
- testing/logging/test_reporting.py::test_log_cli_default_level
- testing/logging/test_reporting.py::test_sections_single_new_line_after_test_outcome

Summary:
Users requested DEFAULT_LOG_FORMAT include `%(name)s` (logger name/module) for improved context in logs. Changing the format affects logging output and some tests failing.

Goal:
Make minimal change to default logging format to include module name while ensuring tests pass. If tests rely on exact formatting, adjust tests or ensure new format is backward-compatible.

Constraints:
- Minimal change surface
- Must include Engineer and QA handoffs

Proposed approach:
1. Locate where DEFAULT_LOG_FORMAT is defined.
2. Update format string to include `%(name)s` before filename, using a format that preserves alignment where possible.
3. Run tests to inspect failures and update expected outputs in tests if the change is intentional and suitable.
4. If tests expect exact previous formatting, we may need to keep old format for CLI or add an option for verbose format; prefer updating tests since user requested improvement.

Tickets:
- T1: Diagnose failures and pinpoint tests asserting the old format
- T2: Implement change in DEFAULT_LOG_FORMAT to include `%(name)s`
- T3: Adjust tests that require exact formatting (only those failing)
- T4: Run full test suite, ensure no regressions
- T5: QA validation

Next: route to Engineer to implement the change and run tests.