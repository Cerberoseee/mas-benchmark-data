Title: Improve default logging format to include module name

Issue: Default logging format in pytest is currently:

DEFAULT_LOG_FORMAT = "%(filename)-25s %(lineno)4d %(levelname)-8s %(message)s"

Proposal: Update DEFAULT_LOG_FORMAT to include the logger name (module path), e.g.

"%(levelname)-8s %(name)s:%(filename)s:%(lineno)d %(message)s"

This makes logs more informative by showing package/module context as well as filename and line number.

Goal: Change default logging format with minimal surface. Ensure all logging-related tests pass; triage failing tests in testing/logging/test_reporting.py.

Plan:
- Diagnostic ticket: run tests to reproduce failures (harness already indicated failing tests.)
- Implementation ticket: update DEFAULT_LOG_FORMAT constant in the logging module.
- Engineer will run test subset and iterate.
- QA to validate tests pass and logs appear as expected.

Risks: Changing default format may affect tests that assert exact output; adjust tests or implementation to preserve expected formatting for CLI outputs.
