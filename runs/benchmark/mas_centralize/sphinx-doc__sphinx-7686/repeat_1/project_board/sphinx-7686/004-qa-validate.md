Title: qa/validate

Goal: Run the test suite (or relevant subset) and confirm the bug is fixed. Provide QA_VERDICT block.

Acceptance criteria:
- QA runs the failing tests and returns QA_VERDICT with verified: true if pass, or verified: false with failing_ids if not.

Assignee: QA
Labels: qa

Notes:
- Run tests: pytest tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module_skipped
- If those pass, run the full autosummary tests.
