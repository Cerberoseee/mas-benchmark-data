Title: 006_engineer_action - Action items for Engineer after QA failure
Owner: Engineer

QA outcome
- QA_VERDICT: verified: false
- failing_ids:
  - test_callable_path (model_fields.test_filepathfield.FilePathFieldTests): test collection failed — pytest not available (bash: pytest: command not found, return code 127)
- notes: QA inspected tests/model_fields/test_filepathfield.py and the implementation. The change appears correct, but QA could not run tests because pytest is not installed in the workspace.

Required Engineer actions
1. Ensure the test runner is available in the workspace so QA can execute tests. Options:
   - Add pytest to the environment (e.g. pip install -U pytest) and verify pytest runs in the workspace PATH.
   - Or provide recorded outputs from a local run of the two commands below (if you cannot install pytest here):
     a) pytest --collect-only tests/model_fields/test_filepathfield.py -q
     b) pytest -q tests/model_fields/test_filepathfield.py::FilePathFieldTests::test_callable_path -q
   - If you cannot make pytest available, explain why and propose an alternate verification plan.

2. Confirm the patch is final (no further code changes). If QA fails the test after pytest is available, fix the failing_ids and re-run.

Notes/constraints
- Tests are applied by the harness; do not modify test files.
- The fix should remain minimal. Avoid broad redesigns.

Deliverables
- Either (A) make pytest available and notify QA to re-run, or (B) provide the two pytest command outputs above for QA to validate.

Return path
- After performing the actions, notify ProjectManager. I will then route to QA for re-run. If QA returns verified: true, I will confirm the patch and close the project.
