Title: QA validation for __version_info__

Description:
Run the test suite for the parsing tests and ensure the package exposes __version_info__ as expected. Provide QA_VERDICT block with verified: true/false and failing_ids if any.

QA tasks:
- Run pytest lib/matplotlib/tests/test_matplotlib.py::test_parse_to_version_info -q
- Confirm all four parameterized cases pass.
- Inspect matplotlib.__version_info__ attribute exists and matches parse_to_version_info(__version__).
- Produce QA_VERDICT block with results and any notes.

Notes:
- If tests failed with collection errors or import errors, see SWE-bench rules: ensure test patch was applied by harness and the engineer didn't modify tests.
- If verified true, ensure a non-empty patch exists (read_patch_diff) before declaring PROJECT COMPLETE.