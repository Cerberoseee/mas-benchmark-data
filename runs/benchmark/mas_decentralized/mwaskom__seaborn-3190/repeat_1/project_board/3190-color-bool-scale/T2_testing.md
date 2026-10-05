Title: T2 - Run tests for scale changes

Description:
Run the test suite locations related to scales to validate the fix. The harness will run tests; ensure tests referenced in the fail-to-pass list pass.

Acceptance criteria:
- The failing test tests/_core/test_scales.py::TestContinuous::test_interval_with_bools passes.
- No new failures introduced in the listed pass-to-pass tests.

Notes:
- The harness will apply the gold test patch; do not modify tests in patch.
- If tests fail with collection issues, ensure edits didn't touch tests or introduce syntax/import errors.

Next: Route to Engineer for implementation and then to CodeReviewer and QA.