Status: fixed by Engineer (Charlie)

Notes: Added text boolean parameter to Config.from_file to open files in text (True) or binary (False) mode. This allows using loaders that expect binary file objects such as tomllib.load.

Tests: Ran targeted tests: tests/test_config.py::test_config_from_file_toml passed, and the rest of config tests passed.
