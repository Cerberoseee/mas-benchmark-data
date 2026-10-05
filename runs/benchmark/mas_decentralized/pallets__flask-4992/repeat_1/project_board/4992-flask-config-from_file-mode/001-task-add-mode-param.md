Title: Engineer: Add file mode parameter to Config.from_file

Description:
Modify flask.Config.from_file to accept an optional parameter that controls the file open mode. Options:
- Add mode: str = "r" default, accepting "r", "rb", etc.
- Or add text: bool = True default (preferable per discussion)

Prefer minimal change: add parameter named "mode" that defaults to "r". Callers can pass mode="rb" for binary.

Tasks:
- Update Config.from_file signature and implementation to use open(joined_path, mode).
- Update docstring and relevant docs.
- Run tests and ensure failing test tests/test_config.py::test_config_from_file_toml passes.

Deliverable: Non-empty patch diff that updates code and tests if needed.

Assign to: Engineer
