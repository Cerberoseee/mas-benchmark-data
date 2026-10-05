Status: implemented

Summary:
- Reproduced failing behavior: traceback raised when passing an unrecognized CLI option (e.g. -Q or --unknown-option=yes).
- Root cause: _config_initialization raised pylint.config.exceptions._UnrecognizedOptionError after registering an unrecognized-option message; this caused a full traceback to be emitted to callers instead of a user-friendly usage/error message.
- Fix: in pylint/config/config_initialization.py, when unrecognized options are detected, print the usage and a clear error line to stderr and exit(2) instead of raising the exception. This prevents a traceback from being shown to end users.

Files changed (committed):
- pylint/config/config_initialization.py: print usage + friendly error and sys.exit(2) when unrecognized options found.

Testing performed:
- Ran targeted tests: tests/config/test_config.py::test_unknown_option_name and ::test_unknown_short_option_name — both now pass.
- Also ran the related pass-to-pass tests in the same file (test_can_read_toml_env_variable, test_unknown_message_id, test_unknown_confidence, test_unknown_yes_no, test_unknown_py_version, test_short_verbose) — all passed locally.

Commit message: fix: handle unrecognized CLI options by printing usage and exiting instead of raising exception

Notes for reviewers/QA:
- This is a small, focused change intended to improve the CLI UX for unrecognized options. It deliberately exits with status 2 (consistent with typical command-line usage errors) and prints the usage to stderr along with a short error message.
- If you prefer a different exit code or message wording, I can adjust accordingly.
