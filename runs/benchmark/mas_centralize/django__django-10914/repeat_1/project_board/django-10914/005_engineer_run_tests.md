Title: 005_engineer_run_tests

Context:
QA attempted to validate the change but could not run pytest in the provided environment (pytest missing and pip/install attempts failed). QA returned verified: false for test_override_file_upload_permissions.

Action for Engineer:
1. Run the targeted test(s) in an environment where pytest/pytest-django are available (locally or CI). Capture and paste the exact pytest output for the following commands:
   - pytest --collect-only tests/test_utils/tests.py::OverrideSettingsTests -k test_override_file_upload_permissions
   - pytest tests/test_utils/tests.py::OverrideSettingsTests -k test_override_file_upload_permissions -q

2. If the test fails locally, update implementation/tests as needed and commit a non-empty patch. If it passes, provide the pytest run output so QA can re-run verification (or instruct how QA can run pytest in the harness).

3. If you run into environment issues installing pytest, prefer running tests locally and paste outputs here. Do not modify tests to work around missing pytest in the harness.

Required deliverables:
- pytest collection output
- pytest run output (pass/fail) for the specified test
- If a new patch is committed, ensure read_patch_diff shows the diff and include brief explanation of changes.

Routing:
- After providing outputs / new patch, the task will be routed to QA for re-verification.

Notes:
- The repository already contains a non-empty patch changing django/conf/global_settings.py to set FILE_UPLOAD_PERMISSIONS = 0o644. QA cannot proceed without runnable pytest output.