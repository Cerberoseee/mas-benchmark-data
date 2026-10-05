Status: Engineer - Fix applied

Notes:
- Implemented one-line change in django/conf/global_settings.py to set FILE_UPLOAD_PERMISSIONS = 0o644.
- Committed change with message: "fix: default FILE_UPLOAD_PERMISSIONS to 0o644".
- Could not run pytest inside the container: pytest is not installed in this environment (bash: pytest: command not found). Please run the targeted tests in CI or install pytest to validate.

Next steps:
- Request CodeReviewer to verify the change and run the test suite in CI.
