Title: Catch invalid regex patterns during config parsing and report clean error

Description:
Catch re.error when compiling user-provided regex options and convert them into argparse-friendly errors so Pylint exits cleanly with an informative message instead of a traceback.

Files likely touched:
- pylint/config/arguments_manager.py
- pylint/config/config_initialization.py

Implementation notes:
- Identify code path where option types for regex are defined (likely a function that compiles the provided pattern via re.compile).
- Wrap re.compile(pattern) in try/except re.error and raise argparse.ArgumentTypeError(f"Invalid regular expression for option {option_name!r}: {err}") or similar.
- Ensure the error is surfaced by argparse such that Pylint exits; do not swallow the error.
- Add unit tests or adjust existing tests expect string to include pattern or option name.

Acceptance criteria:
- tests/config/test_config.py::test_regex_error passes
- tests/config/test_config.py::test_csv_regex_error passes

Estimate: 2h

Assignment: Engineer
