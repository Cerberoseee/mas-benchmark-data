Title: Docs: update FILE_UPLOAD_PERMISSIONS docs and Deployment checklist

Description:
Update the Settings documentation for FILE_UPLOAD_PERMISSIONS and the Deployment checklist to describe the new default (0o644), the reason for the change, and how to restore previous behavior by setting it to None. Add a warning about inconsistent permissions when the setting is omitted.

Acceptance Criteria:
- docs/ref/settings.txt mentions default 0o644 and how to restore old behavior.
- docs/howto/deployment/checklist.txt updated to reference the change.

Estimate: 0.5 engineer-day
