Ticket: Diagnose failing logging tests

Goal: Reproduce and inspect failing tests to determine the impact of changing DEFAULT_LOG_FORMAT.

Tasks:
- Run the failing tests locally: testing/logging/test_reporting.py::test_log_cli_enabled_disabled[True], ::test_log_cli_default_level, ::test_sections_single_new_line_after_test_outcome
- Inspect assertions and snapshots that reference exact formatting
- Decide whether to update tests to match new format or make the default format configurable to preserve previous outputs for certain code paths

Owner: Engineer
Estimate: 2-4h
