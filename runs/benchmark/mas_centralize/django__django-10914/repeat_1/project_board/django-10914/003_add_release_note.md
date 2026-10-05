Title: 003_add_release_note

Goal:
Add a Breaking Change entry to releases/2.2.txt describing the change of default FILE_UPLOAD_PERMISSIONS to 0o644. Include a note that setting it to None restores previous behavior.

Acceptance criteria:
- New bullet in releases/2.2.txt under Breaking changes mentions FILE_UPLOAD_PERMISSIONS default change and migration guidance.

Next: Engineer adds the note when committing code changes.