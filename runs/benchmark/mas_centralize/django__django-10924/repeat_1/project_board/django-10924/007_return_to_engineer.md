Title: 007_return_to_engineer - QA failed to run tests; action required
Owner: Engineer

QA_VERDICT (from QA):
  verified: false
  failing_ids:
    - test_callable_path (model_fields.test_filepathfield.FilePathFieldTests): test collection failed — pytest not available (bash: pytest: command not found, return code 127)
  notes: QA inspected tests/model_fields/test_filepathfield.py and the implementation. The change appears correct and minimal (resolving callable FilePathField.path for form usage), but QA could not run pytest in the workspace so runtime verification is blocked.

Required actions for Engineer (choose one):
1) Install pytest in the workspace and notify ProjectManager to re-run QA. Suggested command:
   - pip install -U pytest
   After installing, confirm by running:
     - pytest --version
   Then reply: "pytest installed — re-run QA" and ProjectManager will route to QA.

2) If you cannot install pytest in this environment, run the following locally (in an env with pytest) and paste the raw outputs (stdout/stderr and return codes) here:
   a) pytest --collect-only tests/model_fields/test_filepathfield.py -q
   b) pytest -q tests/model_fields/test_filepathfield.py::FilePathFieldTests::test_callable_path -q

3) If neither is possible, explicitly request the task be marked blocked/failed and provide rationale. ProjectManager will then close as blocked/failed.

Notes:
- Do NOT modify tests; the harness applies test patches automatically.
- The fix should remain minimal; prefer to evaluate callable path only for form usage (as implemented).

Deliverable after action:
- If (1) or (2): QA will be re-run and must return a QA_VERDICT block. If QA returns verified: true, ProjectManager will confirm the patch and declare PROJECT COMPLETE.
- If (3): ProjectManager will document the blocked/failed state and close the task.
