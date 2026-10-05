Implementation summary

Files changed:
- pylint/config/argument.py
  - Added _regexp_transformer to compile regex strings and raise argparse.ArgumentTypeError with a friendly message when re.error occurs.
  - Updated _regexp_csv_transfomer to use _regexp_transformer for each item.
  - Updated _TYPE_TRANSFORMERS to use the new transformer for 'regexp'.

- pylint/config/option.py
  - Updated _regexp_validator to catch re.error and raise optparse.OptionValueError with a friendly message.

Behavior:
- Invalid regular expressions in config options now produce a clear, non-traceback error message and exit cleanly.
- The messages normalize positional information to 'beginning at index N' when available.

Test results (local):
- pytest tests/config/test_config.py::test_regex_error - passed
- pytest tests/config/test_config.py::test_csv_regex_error - passed
- Additional related config tests also passed locally.

Next step: Code review (T4).