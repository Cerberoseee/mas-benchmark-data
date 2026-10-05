Issue: Traceback printed for unrecognized option

Repository: pylint-dev/pylint
Issue details: When an unrecognized option (e.g. `pylint -Q`) is passed, pylint prints a helpful lint message but also raises and prints a traceback for _UnrecognizedOptionError_. The desired behavior is to suppress the internal traceback and instead show a concise usage/error message (similar to mypy) and exit cleanly.

Failing tests:
- tests/config/test_config.py::test_unknown_option_name
- tests/config/test_config.py::test_unknown_short_option_name

Passing related tests:
- tests/config/test_config.py::test_can_read_toml_env_variable
- tests/config/test_config.py::test_unknown_message_id
- tests/config/test_config.py::test_unknown_confidence
- tests/config/test_config.py::test_unknown_yes_no
- tests/config/test_config.py::test_unknown_py_version
- tests/config/test_config.py::test_short_verbose

Goal: implement a minimal change to avoid printing the traceback for unrecognized option errors and provide a clean error message and non-zero exit code. Create focused tickets for investigation, implementation, review, and QA.