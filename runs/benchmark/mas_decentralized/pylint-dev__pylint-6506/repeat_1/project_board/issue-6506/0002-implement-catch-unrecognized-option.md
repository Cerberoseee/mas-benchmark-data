Title: Implement handling for UnrecognizedOptionError to avoid traceback

Description:
After investigation, implement a minimal change to catch UnrecognizedOptionError at the CLI top-level or config initialization boundary, print a concise error message (matching existing lint message), and exit with a non-zero code without emitting a traceback.

Acceptance criteria:
- Tests tests/config/test_config.py::test_unknown_option_name and test_unknown_short_option_name pass.
- No other tests regressing.
- Change minimal and well-scoped (prefer changes in pylint/__init__.py or lint/run.py near the invocation boundary).

Assign to: Engineer
Labels: bug, fix
Estimated time: 1-3h

Notes:
- Ensure that other exceptions still show tracebacks for debugging.
- Prefer to reuse existing message formatting where possible (the earlier lint message is already printed by the checker). Print a friendly usage hint if helpful.