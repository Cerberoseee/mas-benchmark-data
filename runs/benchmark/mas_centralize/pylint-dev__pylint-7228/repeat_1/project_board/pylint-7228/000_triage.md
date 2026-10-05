Title: Regex \p{...} in pylintrc causes crash during config parsing

Summary:
When a user sets option regexes in pylintrc that include unsupported escapes like "\p{Han}", Python's re.compile raises re.error leading to an uncaught exception and a full traceback. Instead, Pylint should catch invalid regex patterns during configuration parsing and exit cleanly with a helpful error message.

Reproduction:
- Add to pylintrc: function-rgx=[\p{Han}a-z_][\p{Han}a-z0-9_]{2,30}$
- Run pylint
- Observe unhandled re.error stacktrace

Desired behavior:
- Pylint exits with a user-friendly error indicating the invalid regex and its location (option name)
- Tests to add/adjust: tests/config/test_config.py::test_regex_error and ::test_csv_regex_error should pass

Constraints and notes:
- We must not silently accept invalid regexes. The process should exit non-zero but not show a raw stacktrace.
- Minimal surface changes: catch re.error during parsing of regex options and raise argparse.ArgumentTypeError or otherwise cause parser to handle cleanly.
- Existing tests for unknown options should still behave as before.

Initial diagnosis pointers:
- The crash happens during argparse parsing where re.compile is used to cast option values to regex objects.
- Search for location(s) where regex type is used in arguments parsing (likely in config/arguments_manager.py or config/config_initialization.py) and wrap re.compile in try/except re.error.
- Look for helper that converts a string to a compiled regex (maybe config/arguments_manager or a util). Add user-facing error message.

Next steps (tickets):
1) Implement: catch re.error when compiling regex options and re-raise as argparse.ArgumentTypeError with helpful message.
2) Unit tests: Ensure test_regex_error and test_csv_regex_error assert proper exit and message; update expected message if necessary.
3) Reviewer: Code review of the small change.
4) QA: Run full test subset; ensure pass-to-pass tests still pass.

Routing:
- Engineer: implement change (small try/except) and run tests
- CodeReviewer: confirm exception type and message is appropriate
- QA: run failing tests and full config tests

Estimate: 1d
