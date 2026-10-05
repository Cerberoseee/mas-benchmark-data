Title: Code review - RST header_rows support

Description:
Review the implementation patch that adds header_rows support to the RST
writer. Ensure behavior mirrors fixed_width writer where appropriate, check for
edge cases, and confirm minimal change surface.

Checklist:
- __init__ signature updated appropriately.
- Rendering logic includes header_rows with correct alignment and borders.
- No tests modified unintentionally.
- Diff is minimal and backward-compatible.

Assignee: CodeReviewer
