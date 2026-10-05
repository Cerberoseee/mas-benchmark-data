Status: In progress

Update: Changed default FILE_UPLOAD_PERMISSIONS to 0o644 in django/conf/global_settings.py to make uploaded file permissions consistent across upload handlers.

Files changed:
- django/conf/global_settings.py: FILE_UPLOAD_PERMISSIONS = 0o644 (was None)

Notes:
- Implemented minimal change. Committed locally.
- Could not run pytest in container: pytest not installed (python -m pytest failed).

Next steps:
- Reviewer should run the specified Fail-to-pass and Pass-to-pass tests in an environment with pytest installed and verify other behavior.
