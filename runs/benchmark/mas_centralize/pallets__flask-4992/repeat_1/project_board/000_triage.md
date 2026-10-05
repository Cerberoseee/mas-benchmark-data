Title: Add file mode / text flag to flask.Config.from_file()

Summary:
The method flask.Config.from_file currently opens files in text mode. Python 3.11's tomllib expects a binary file object. Add a parameter to from_file to allow opening files in binary mode (or a text flag), so callers can pass tomllib.load directly.

Scope:
- Modify Config.from_file to accept a new optional parameter controlling file mode. Minimal API: mode: str = "r" (or text: bool = True).
- Ensure backwards compatibility: default behavior should remain text mode.
- Update tests to expect that test_config_from_file_toml passes without workaround.
- Write unit tests covering binary mode / text flag behavior.

Constraints:
- Minimal changes to implementation; do not redesign config loading.
- Ensure no public API breaking changes beyond additive optional parameter.

Initial plan:
1) Implement change in src/flask/config.py where Config.from_file is defined.
2) Run tests and iterate until passing.
3) Create PR and request review.

Assignee: unassigned
Status: triaged
