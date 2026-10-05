Title: Investigate why UnrecognizedOptionError traceback is printed

Description:
Reproduce the failure locally by running pytest for the two failing tests. Determine where _UnrecognizedOptionError is raised and why it is not handled gracefully. Identify the minimal location(s) to catch the error and convert it into a user-friendly message and exit code without printing a traceback.

Acceptance criteria:
- Reproduction steps documented.
- The stack location(s) where the exception is raised and propagated are identified.
- A recommended minimal change set (files/functions) is proposed for implementing the fix.

Assign to: Engineer
Labels: investigation, bug
Estimated time: 1-2h

Notes:
Failing tests:
- tests/config/test_config.py::test_unknown_option_name
- tests/config/test_config.py::test_unknown_short_option_name

Start by searching for _UnrecognizedOptionError class and its usages; check config_initialization.py and the top-level cli/run entrypoints.