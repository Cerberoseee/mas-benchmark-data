Title: 004_docs_update

Goal:
Update documentation text for FILE_UPLOAD_PERMISSIONS in settings docs and deployment checklist to clarify that uploaded files may get 0o600 without this setting and to recommend setting FILE_UPLOAD_PERMISSIONS=0o644 as default.

Acceptance criteria:
- Relevant docs updated.
- Not required for SWE-bench run if docs are not within the test harness.

Next: Implement if docs present in repo; otherwise skip.