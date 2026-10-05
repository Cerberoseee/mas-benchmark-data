Status: implemented

Change: Set default FILE_UPLOAD_PERMISSIONS to 0o644 in django/conf/global_settings.py.

Details:
- Modified django/conf/global_settings.py: replaced FILE_UPLOAD_PERMISSIONS = None with FILE_UPLOAD_PERMISSIONS = 0o644.
- Committed the change to the repo (local commit).

Testing:
- Intended validation: run pytest collect-only on tests/test_utils/tests.py and run the targeted test test_override_file_upload_permissions.
- Current environment: pytest is not available in the container (ImportError: No module named pytest), so I could not run the test commands here.

Next steps for CodeReviewer/CI:
- Run `pytest tests/test_utils/tests.py::OverrideSettingsTests::test_override_file_upload_permissions -q` in CI or a dev environment with pytest installed to validate the fix.
- Also run the listed pass-to-pass tests afterwards.

Notes:
- This is a minimal behavior change as requested. If reviewer prefers this change to be targeted to a different release/branch or to also change FILE_UPLOAD_DIRECTORY_PERMISSIONS, let me know and I will adjust accordingly.
