Title: Code review: Domain column change for `flask routes`

Goal:
Review the implementation patch for correctness, style, and minimal change surface.

Checklist:
- Code is small and contained to CLI output formatting.
- Uses Rule.host and Rule.subdomain appropriately; avoids relying on SERVER_NAME unless tests expect it.
- No changes to public APIs other than CLI output formatting.
- Tests updated only if absolutely necessary (should not be).

Assign to: CodeReviewer (transfer_to_codereviewer)