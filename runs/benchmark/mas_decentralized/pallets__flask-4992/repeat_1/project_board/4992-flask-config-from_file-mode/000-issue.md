Title: Add file mode parameter to flask.Config.from_file()

Description:
Python 3.11's tomllib.load accepts a binary file object, but flask.Config.from_file() currently opens files in text mode. This prevents direct use of tomllib.load as the loader when calling from_file. Add a parameter to from_file (e.g., mode or text=True/False) to allow binary mode opening.

Goals:
- Allow users to specify whether files passed to Config.from_file should be opened in text or binary mode.
- Preserve backward compatibility and minimal API surface changes.
- Update tests to reflect behavior.

Constraints:
- Keep changes minimal and focused to Config.from_file.
- Ensure tests pass and document new parameter in changelog/ docs.

Related tests:
- tests/test_config.py::test_config_from_file_toml (currently failing)
