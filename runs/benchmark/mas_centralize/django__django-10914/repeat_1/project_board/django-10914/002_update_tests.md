Title: 002_update_tests

Goal:
Update tests that expect old None default for FILE_UPLOAD_PERMISSIONS to reflect new default of 0o644.

Acceptance criteria:
- test_utils.tests.OverrideSettingsTests::test_override_file_upload_permissions updated to expect 0o644 by default if appropriate.
- Ensure any other tests referencing FILE_UPLOAD_PERMISSIONS are adjusted.

Files to inspect:
- tests/utils_tests/test_override_settings.py or similar path in test_utils.tests

Estimate: small

Next: Engineer updates tests alongside implementation to keep CI green.