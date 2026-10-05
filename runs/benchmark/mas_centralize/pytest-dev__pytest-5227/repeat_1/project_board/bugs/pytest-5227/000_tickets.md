Tickets for bug pytest-5227:

1) Triage & identify locations
- Find where DEFAULT_LOG_FORMAT is defined and used.
- Confirm tests failing due to format change.
- Estimate change surface.

2) Implement minimal change
- Update DEFAULT_LOG_FORMAT to include %(name)s (logger name).
- Ensure format remains compatible with existing tests that match strings: consider providing alternative format when log_cli formatting differs.

3) Run full test subset locally (CI) for logging tests
- Run failing tests and other logging tests.

4) Fix tests or adjust implementation for backward compatibility
- If tests assert exact format, update formatting logic to preserve existing behavior for those code paths.

5) Code review
- Small review of diff for scope & backward compatibility.

6) QA
- Run pytest test suite subset; provide QA_VERDICT block.

7) Finalize
- Ensure patch exists and non-empty; prepare final summary.

Ownership flow: Engineer -> CodeReviewer -> QA -> ProjectManager

Files touched likely: _pytest/logging.py or related module. Search for DEFAULT_LOG_FORMAT constant.
