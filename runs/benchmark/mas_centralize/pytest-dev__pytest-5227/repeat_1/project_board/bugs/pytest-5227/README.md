Title: Improve default logging format

Repository: pytest-dev/pytest
Issue: Suggestion to include module name in DEFAULT_LOG_FORMAT instead of only filename. Some tests currently failing after changing format.

Goal: Update default logging format to include logger name (module) and ensure all logging-related tests pass with minimal changes.

Deliverables:
- Small patch to change DEFAULT_LOG_FORMAT in relevant module(s).
- Adjust tests if they rely on exact format, but prefer to make formatting change backwards compatible where possible.
- Engineer, CodeReview, QA workflow: implement -> review -> test -> finalize.

Notes:
- Failures observed in testing/logging/test_reporting.py::test_log_cli_enabled_disabled[True], test_log_cli_default_level, test_sections_single_new_line_after_test_outcome
- Many logging tests already pass.
- Avoid modifying test files unless necessary; prefer conservative change to default format or where output is formatted for CLI only.
