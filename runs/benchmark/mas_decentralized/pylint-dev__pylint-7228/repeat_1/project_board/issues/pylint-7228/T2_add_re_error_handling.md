T2 - Implement: catch re.error when compiling config regexes

Objective:
Wrap re.compile calls for configuration regex options so that if re.error is raised, pylint exits cleanly with a helpful error message describing the offending option and pattern.

Requirements:
- Do not change the behavior of exiting on invalid regex; still exit non-zero.
- Message should be concise and user friendly, similar to unknown option handling.
- Minimal code changes; prefer local try/except blocks near existing compilation code.

Acceptance criteria:
- Tests tests/config/test_config.py::test_regex_error and ::test_csv_regex_error pass.
- No other tests regressed.

Assignee: Engineer