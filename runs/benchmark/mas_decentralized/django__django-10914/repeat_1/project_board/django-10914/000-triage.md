Triage notes:
- Change: set default FILE_UPLOAD_PERMISSIONS to 0o644 per ticket discussion.
- Tests affected: test_override_file_upload_permissions.
- Environment does not have pytest installed, so local validation could not be performed in container.
- Committed change to django/conf/global_settings.py.
