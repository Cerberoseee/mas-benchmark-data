Title: Tests: adjust tests expecting FILE_UPLOAD_PERMISSIONS default None

Description:
Update tests that currently assume FILE_UPLOAD_PERMISSIONS is None. Specifically, update test_override_file_upload_permissions in test_utils.tests.OverrideSettingsTests to expect 0o644 default or set the setting explicitly in the test to preserve previous behavior.

Acceptance Criteria:
- test_override_file_upload_permissions passes under new default.
- No other tests rely on None; if so, adjust similarly.

Files likely to change:
- tests/utils_tests/...(path from failing test)

Estimate: 0.5 engineer-day

