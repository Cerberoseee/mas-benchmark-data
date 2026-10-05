Engineer patch applied

Summary of changes:
- Modified src/flask/config.py to add a `text: bool = True` kw-only parameter to Config.from_file and open the file in 'r' or 'rb' mode accordingly.
- All tests in tests/test_config.py pass locally for the changed tests.

Commit: 9293bcbec574fec17bd8ca02b4098d54353b19b7
