Ticket: 0004-qa - Validate fix for ignore-paths with recursive current dir

Goal:
Validate the fix against the failing test and with a small manual repro using both `pylint --recursive=y src/` and `pylint --recursive=y .` on Windows-style paths (simulate './src/gen' roots).

Acceptance criteria:
- QA_VERDICT block present with verified: true if tests pass and repros are checked on both path forms.
- If failing, QA returns verified: false with failing_ids and notes.

Steps for QA:
1. Pull the branch after CodeReviewer approves and deploy locally.
2. Run pytest tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir
3. Create small repro as in issue: src/gen/test.py with import bla and pyproject.toml ignore-paths containing '^src/gen/.*$'. Run both `pylint --recursive=y src/` and `pylint --recursive=y .` and confirm no errors reported.
4. Provide QA_VERDICT block in the results.

Assignee: QA
