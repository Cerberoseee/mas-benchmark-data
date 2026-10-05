Title: Triage and diagnose unrecognized option traceback

Goal:
Reproduce failing tests and locate where UnrecognizedOptionError is raised and why a traceback is printed.

Tasks:
- Run the two failing tests:
  - tests/config/test_config.py::test_unknown_option_name
  - tests/config/test_config.py::test_unknown_short_option_name
- Run pytest --maxfail=1 -k test_unknown_option_name -q to reproduce quickly.
- Inspect pylint/config/config_initialization.py to find where _UnrecognizedOptionError is raised.
- Determine how exception is handled by the CLI (pylint/lint/run.py or __init__.py).
- Create minimal proposal for handling the exception gracefully (catch and print friendly message, exit non-zero without traceback).

Deliverables:
- Short diagnosis notes and proposed change lines.
