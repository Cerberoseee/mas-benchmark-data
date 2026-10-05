T-006: Implemented Config.from_file text mode parameter

I added text: bool = True to src/flask/config.py:Config.from_file. This allows callers to open files in binary mode (text=False) for loaders that require it, e.g. tomllib.load.

Committed change: feat: add text mode option to Config.from_file

Tests: tests/test_config.py::test_config_from_file_toml now passes.
