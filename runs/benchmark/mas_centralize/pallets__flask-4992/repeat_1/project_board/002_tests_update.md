Title: Add tests for Config.from_file mode support

Description:
Add/modify tests to ensure that Config.from_file can accept binary loaders such as tomllib.load by allowing opening files in binary mode.

Tasks:
- Update tests/test_config.py::test_config_from_file_toml to call from_file(..., mode="rb") or use new text flag as appropriate.
- Add tests to ensure default behavior remains text mode (e.g., json loader still works).

Assignee: Engineer
Status: todo
