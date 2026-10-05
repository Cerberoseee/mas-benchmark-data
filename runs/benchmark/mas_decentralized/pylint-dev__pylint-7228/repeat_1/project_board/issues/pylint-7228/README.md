Issue: rxg include '\p{Han}' will throw error

Repository: pylint-dev/pylint

Description:
A user reported that specifying a regex containing "\p{Han}" in pylintrc, e.g.

function-rgx=[\p{Han}a-z_][\p{Han}a-z0-9_]{2,30}$

causes pylint to crash with a traceback originating from re.compile, raising re.error: bad escape \p at position 1.

Goal:
- Ensure pylint reports a friendly error message when a regex in configuration is invalid (re.error) instead of crashing with a full traceback.
- Keep behavior of exiting on invalid regex; do not silently ignore invalid patterns.

Related failing tests:
- tests/config/test_config.py::test_regex_error
- tests/config/test_config.py::test_csv_regex_error

Constraints:
- Minimal change surface targeted to configuration parsing where regex options are interpreted.
- Typical flow: Engineer -> CodeReviewer -> QA.

Plan:
1. Investigate where configuration options that expect regexes are parsed/validated.
2. Add try/except around re.compile calls to catch re.error and raise a user-friendly SystemExit with a clear message about which option and pattern failed.
3. Add targeted unit tests (already present as failing) should pass after fix.
4. Create small focused commits and route for review.

Tickets to create:
- T1: Diagnose: locate code path and confirm where re.compile is called for config patterns.
- T2: Implement: add error handling for re.error, produce friendly exit message.
- T3: Tests: ensure tests expecting friendly error pass; run test suite locally.
- T4: Code review: reviewer to check change scope and messaging.
- T5: QA: run CI tests and verify failing tests pass.

Owner: Alice (project manager).