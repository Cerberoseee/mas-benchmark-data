Title: Review patch for BoundaryNorm-safe format_cursor_data
Assignee: CodeReviewer

Description:
Review the Engineer's patch implementing special handling for BoundaryNorm in lib/matplotlib/artist.py. Check for:
- Correctness of logic for finding neighboring interval values
- Proper handling of clip/extend/bounds
- Minimal change surface and code style
- Adequate tests and comments

If acceptable, transfer directly to QA (transfer_to_qa). If blocking issues, return to Engineer with REVIEW_VERDICT containing blocking_findings: true and comments.
